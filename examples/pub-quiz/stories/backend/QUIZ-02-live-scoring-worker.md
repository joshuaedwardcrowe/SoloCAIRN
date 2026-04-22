# Story: QUIZ-02 Live Scoring Worker

## Context

When a team submits an answer, the server must score it, update the team's cumulative score, and broadcast a leaderboard update. This story is that worker.

See [04-architecture.md](../../04-architecture.md) §Components for the design and §Key decisions for the authoritative-server rationale.

## Acceptance criteria

- [ ] `POST /sessions/{code}/answers` accepts answer submissions from teams with a valid team token.
- [ ] Correct answer = 10 points. Incorrect = 0. First correct on each question earns a +5 speed bonus.
- [ ] Duplicate submissions for the same question by the same team are rejected with a clear error.
- [ ] Submissions arriving after `ANSWER_REVEALED` are rejected.
- [ ] Scoring is eventually consistent within 200ms of submission under normal load.
- [ ] `LEADERBOARD_UPDATED` event is emitted after each score change, debounced to at most once every 250ms per session.
- [ ] Paper teams: scores submitted per-round via a separate endpoint (`POST /sessions/{code}/paper-scores`) and folded into the same leaderboard.
- [ ] Scoring behind a feature flag so the algorithm can be iterated on without a release.

## Files likely touched

- `api/src/workers/quiz-scoring.ts` (new)
- `api/src/services/quiz-scoring.ts` (new)
- `api/src/routes/quiz-answers.ts` (new)

## Dependencies

- Depends on: [QUIZ-01](QUIZ-01-session-service.md), [QUIZ-08](../database/QUIZ-08-schema.md)

## Out of scope

- Tiebreakers at quiz end (see Q8 in open questions).
- Custom scoring rules per quiz (v2).

## Notes

- Speed bonus: compute from server-side timestamps only. Client-reported timestamps are untrusted.
- The debounce on `LEADERBOARD_UPDATED`: we expect bursts of submissions right after a question is shown. Debounce protects the clients from update storms.
- Paper team endpoint: host-only, enforced via same auth as QUIZ-01 host actions.
