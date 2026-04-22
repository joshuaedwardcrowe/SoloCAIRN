# Story: QUIZ-01 Session Service

## Context

The session service owns the lifecycle of a quiz session: create, join, advance, reveal, end. All other backend work depends on this service existing.

See [04-architecture.md](../../04-architecture.md) §Components for the design.

## Acceptance criteria

- [ ] `POST /sessions` creates a session from a host-provided quiz template and returns a session code.
- [ ] `POST /sessions/{code}/join` lets a team join by submitting a team name. Returns a team token.
- [ ] `POST /sessions/{code}/advance` moves the session to the next question. Rejected if the caller is not the host.
- [ ] `POST /sessions/{code}/reveal` reveals the correct answer for the current question.
- [ ] `POST /sessions/{code}/end` closes the session.
- [ ] WebSocket topic `sessions/{code}` broadcasts events: `QUESTION_SHOWN`, `ANSWER_REVEALED`, `LEADERBOARD_UPDATED`, `SESSION_ENDED`.
- [ ] State held in Redis with snapshot to Postgres every 30 seconds and on every round boundary.
- [ ] Long-poll fallback at `GET /sessions/{code}/events?since=<cursor>` returns events missed since cursor.
- [ ] Host authentication enforced on host-only actions.
- [ ] Session codes are 6 characters, short-lived (24 hours), collision-checked at creation.

## Files likely touched

- `api/src/services/quiz-session.ts` (new)
- `api/src/routes/quiz-sessions.ts` (new)
- `api/src/websockets/quiz.ts` (new)
- `api/src/workers/session-snapshotter.ts` (new)
- `api/src/auth/host.ts` (new)

## Dependencies

- Depends on: [QUIZ-08](../database/QUIZ-08-schema.md) (schema)
- Consumed by: QUIZ-02, QUIZ-03, QUIZ-04, QUIZ-05, QUIZ-06, QUIZ-07

## Out of scope

- Scoring logic (QUIZ-02).
- Question selection or rendering (QUIZ-03).
- Any client-side work.
- Auth beyond a simple host token for v1.

## Notes

- Use the existing Redis client from `api/src/infrastructure/redis.ts`.
- Follow the existing route structure in `api/src/routes/`.
- WebSocket handling pattern: see `api/src/websockets/README.md` in the repo.
- Session code generation: use the existing short-code utility; verify uniqueness in Redis.
