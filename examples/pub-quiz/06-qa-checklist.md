# QA Checklist: Pub Quiz Live Scoring

> Owned by QA. Updated through the Story PR review and as bugs surface during build.
> Repo-wide concerns (security baseline, accessibility AA baseline) live in `docs/checklists/`. This file is feature-specific.

## Functional: end-to-end happy path

- [ ] Host can create a session from a pre-built template and see a session code.
- [ ] Players can scan the QR code, land on the join screen, and create a team.
- [ ] Players can join an existing team from the team list.
- [ ] Host advances through all questions; venue display updates within 1 second.
- [ ] Players see each question on their phones within 1 second of advance.
- [ ] Player answers are accepted, scored, and reflected on the leaderboard.
- [ ] Speed bonus awarded only to the first correct submission per question.
- [ ] Final leaderboard shows correct totals at session end.

## Functional: per-story acceptance

For each story, every acceptance criterion has been verified in isolation. Tracked per Code PR; this section confirms the rollup before pilot.

- [ ] [QUIZ-01](stories/backend/QUIZ-01-session-service.md) acceptance criteria all green
- [ ] [QUIZ-02](stories/backend/QUIZ-02-live-scoring-worker.md) acceptance criteria all green
- [ ] [QUIZ-03](stories/backend/QUIZ-03-question-bank-api.md) acceptance criteria all green
- [ ] [QUIZ-04](stories/frontend/QUIZ-04-host-console.md) acceptance criteria all green
- [ ] [QUIZ-05](stories/frontend/QUIZ-05-venue-display.md) acceptance criteria all green
- [ ] [QUIZ-06](stories/mobile/QUIZ-06-player-join-flow.md) acceptance criteria all green
- [ ] [QUIZ-07](stories/mobile/QUIZ-07-player-answer-ui.md) acceptance criteria all green
- [ ] [QUIZ-08](stories/database/QUIZ-08-schema.md) migration runs cleanly forward and back

## Data and state

- [ ] Session code is unique and 6 characters; collisions handled at creation.
- [ ] Team token cannot be reused by a different team.
- [ ] Duplicate answer submission for the same question is rejected with a clear error.
- [ ] Submissions arriving after `ANSWER_REVEALED` are rejected (server-side check, not client trust).
- [ ] Paper team scores fold into the leaderboard with the same totals logic.
- [ ] Snapshot to Postgres occurs at the documented cadence and on round boundaries.
- [ ] On simulated server restart, session resumes from the most recent snapshot.

## Connectivity edges

- [ ] WebSocket connects on a healthy network.
- [ ] Long-poll fallback engages when WebSocket is blocked (simulated by blocking upgrades).
- [ ] Host console connection indicator transitions correctly: green to yellow to red and back.
- [ ] Player who loses signal mid-question recovers and their queued submission lands; if too late, they see the non-blaming message.
- [ ] Player closing and reopening the tab rejoins via the persisted token (no re-name).
- [ ] Venue display reconnects automatically without a page reload.

## Concurrency and load

- [ ] 50 simultaneous players in a single session: scoring stays within the 200ms target.
- [ ] Burst of 50 simultaneous answer submissions in the first 2 seconds after a question is shown does not produce update-storm flicker on the venue display.
- [ ] Two hosts cannot operate the same session at once (host token enforced).
- [ ] Concurrent join requests with the same team name are handled (first wins, second sees a clear collision message).

## UX states (every surface)

For host console, venue display, and player app:

- [ ] Loading state visible whenever waiting on the network.
- [ ] Empty state for first session, first team, no questions remaining.
- [ ] Error state with a clear next action.
- [ ] Success state where applicable.

## Host console specifics

- [ ] Spacebar advances the question.
- [ ] Pause and resume work; the timer pauses with them.
- [ ] Paper-team add and score-entry flow is reachable and obvious.
- [ ] Connection indicator is always visible.
- [ ] Reveal action is a deliberate two-step (no accidental reveals).

## Venue display specifics

- [ ] Question text readable at 5 metres on a 1080p TV.
- [ ] Contrast ratio at or above 7:1 for body text.
- [ ] Leaderboard position changes animate smoothly enough to follow.
- [ ] No interactive controls present.
- [ ] Idle state (between questions) does not look like a bug.

## Player app specifics

- [ ] Tap targets at least 48px on the smallest supported device.
- [ ] Works on iOS Safari (min iOS 15) and Chrome on Android (min Chrome 100).
- [ ] Answer can be changed before submission, locked after.
- [ ] After reveal: own correctness, correct answer, current score, current rank all visible.
- [ ] Profanity filter rejects expected inputs without false positives on common names.

## Accessibility

- [ ] Player app: keyboard navigation works, focus order is logical.
- [ ] Player app: screen reader announces question, options, and result.
- [ ] Host console: screen reader announces connection state changes.
- [ ] Colour is not the only way correctness is indicated on the player feedback screen.
- [ ] All form inputs have visible labels.

## Performance

- [ ] First question after start: visible on all surfaces within the latency budget.
- [ ] Leaderboard update under burst load does not block input on the player app.
- [ ] Bundle size for player app stays under the team's documented budget.

## Observability

- [ ] Per-session event log captures the lifecycle.
- [ ] Metric emitted for connected client count per session.
- [ ] Metric emitted for scoring latency.
- [ ] Alert defined for "scoring queue depth above threshold."
- [ ] Runbook covers the top two failure modes: scoring worker down, in-memory store down.

## Release

- [ ] Feature flag verified to enable and disable cleanly per venue.
- [ ] Rollback procedure tested on staging.
- [ ] Pilot venues briefed; pilot success criteria from [03-scope.md](03-scope.md) reviewed.
- [ ] Open questions in [05-open-questions.md](05-open-questions.md) all closed before pilot.
- [ ] Stakeholders informed of the rollout window.

## Sign-off

- [ ] QA: feature meets the criteria above.
- [ ] Team Lead: scope and architecture intent satisfied.
- [ ] UX: design intent satisfied on every surface.

When all three sign, the feature is ready for the pilot. Pilot results determine wider rollout.
