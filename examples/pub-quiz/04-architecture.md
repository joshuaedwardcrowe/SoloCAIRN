# Architecture: Pub Quiz Live Scoring

## Linked artifacts

- Problem statement: [00-problem-statement.md](00-problem-statement.md)
- Scope: [03-scope.md](03-scope.md)

## Overview

A single backend service exposes an HTTP API for session management and a WebSocket endpoint for real-time events. Three clients connect:

- The **host console** (web SPA) on the host's laptop or tablet.
- The **venue display** (web SPA) on the TV.
- The **player app** (mobile web) on each player's phone.

All clients subscribe to session events via WebSocket and fall back to HTTP polling when WebSocket is unavailable. Scoring happens on the server on every answer submission; the resulting state is broadcast to all subscribers.

## Diagram

```
 Host laptop             Venue TV             Player phones
+-----------+          +-----------+         +-----------+
| Host      |          | Venue     |         | Player    |
| Console   |          | Display   |         | App       |
+-----+-----+          +-----+-----+         +-----+-----+
      |                      |                     |
      |   WebSocket + HTTP (fallback: long-poll)   |
      +-----------+----------+----------+----------+
                  |                     |
                  v                     v
          +-----------------------------------+
          |        Quiz Backend Service       |
          |  +-----------+   +--------------+ |
          |  | Session   |   | Scoring      | |
          |  | Service   |   | Worker       | |
          |  +-----+-----+   +------+-------+ |
          |        |                |         |
          |        v                v         |
          |  +-----------------------------+  |
          |  |   Database (sessions,       |  |
          |  |   answers, questions,       |  |
          |  |   scores)                   |  |
          |  +-----------------------------+  |
          +-----------------------------------+
```

## Key decisions

### Decision 1: WebSocket with HTTP fallback

- **Choice.** WebSocket for realtime, HTTP long-polling as fallback.
- **Alternatives considered.** SSE (server-sent events); short-polling; WebRTC.
- **Why this one.** WebSocket is the lowest-latency option that all our target browsers support. HTTP fallback addresses pub wifi that blocks WebSocket upgrades on some captive portals.
- **Tradeoffs we accept.** Two code paths to maintain on the backend. We accept this because the fallback directly addresses one of the top-cited research concerns (wifi).

### Decision 2: Authoritative server for scoring

- **Choice.** The server computes scores. Clients display only what the server tells them.
- **Alternatives considered.** Client-side scoring with server reconciliation; trust-but-verify.
- **Why this one.** Cheating resistance is weak in a pub quiz, but trivial tampering (edit local state in devtools) would make the leaderboard a joke. Server-authoritative is simpler and removes the whole class of issue.
- **Tradeoffs we accept.** Slightly higher server load per event. Fine at our scale.

### Decision 3: Session state held in-memory with DB snapshot

- **Choice.** Active session state lives in Redis-style in-memory store with periodic DB snapshotting. DB is the durable record for post-quiz analysis.
- **Alternatives considered.** Every event written to DB immediately; full session in DB with in-memory caching.
- **Why this one.** Latency budget per event is tight (sub-second). In-memory reads and writes are an order of magnitude faster. Snapshots every 30 seconds and on every round boundary give us enough durability for this use case.
- **Tradeoffs we accept.** In the rare event of a server crash mid-round, we may lose up to 30 seconds of answer submissions. Acceptable for this product; documented in the runbook.

### Decision 4: Mobile web, not native, in v1

- **Choice.** The player app is a mobile-web app served from the same domain as the other clients.
- **Alternatives considered.** Native Android + iOS apps; PWA with install prompt.
- **Why this one.** QR-scan-to-join is the desired flow. App store installs are friction-heavy for a one-off evening. The player flow is simple enough that web is adequate.
- **Tradeoffs we accept.** No push notifications, no offline-first benefits. Evaluated again in v2.

## Components

### Session Service

- **Responsibility.** Manages the lifecycle of a quiz session: create, join, advance, reveal, end.
- **Interface.** HTTP endpoints for lifecycle actions; WebSocket topic per session for events.
- **Dependencies.** In-memory store (Redis), Database (Postgres), Question Bank API.
- **Failure modes.** If the in-memory store fails, session state is lost; the host can resume from the last snapshot (up to 30 seconds behind). Players can rejoin.

### Live Scoring Worker

- **Responsibility.** Receives answer submissions, computes scores, updates the in-memory store, and broadcasts leaderboard updates.
- **Interface.** Consumes answer events, writes score events.
- **Dependencies.** In-memory store, event bus.
- **Failure modes.** If the worker fails, answers queue up. If queue exceeds threshold, host sees a warning in the console.

### Question Bank API

- **Responsibility.** Serves questions from the pre-built bank.
- **Interface.** HTTP endpoints for listing, selecting, and fetching questions.
- **Dependencies.** Database.
- **Failure modes.** If questions cannot be fetched, session creation fails with a clear error.

## Data

New tables (see [stories/database/QUIZ-08-schema.md](stories/database/QUIZ-08-schema.md) for detail):

- `quiz_sessions`: one row per session.
- `quiz_teams`: teams joining a session.
- `quiz_answers`: each answer submitted.
- `quiz_questions`: the bank.
- `quiz_scores`: materialised leaderboard snapshots.

## External dependencies

- **Database**: Postgres (existing).
- **In-memory store**: Redis (existing).
- **Hosting**: existing cloud environment.

No new third-party services in v1.

## Non-functional considerations

- **Performance.** Target: 95th percentile latency from host "next question" to all clients displaying the new question under 500ms on a healthy network. Under 2s on a degraded network.
- **Security.** Session join is via a short-lived, session-scoped code. No player accounts in v1. Host actions require host authentication.
- **Observability.** Per-session event log. Metrics for connected clients, answer submission rate, scoring latency.
- **Accessibility.** Player mobile web: WCAG AA. Venue display is optimised for readability at distance; not a primary interactive surface.

## Rollout

- Feature behind a flag, enabled per venue.
- Pilot at three venues for two weeks each.
- Gradual enablement after pilot.
- Rollback: disable the flag. Falls back to the current paper-only flow.

## Open questions

See [05-open-questions.md](05-open-questions.md).
