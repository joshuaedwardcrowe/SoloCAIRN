# Story: QUIZ-07 Player Answer UI

## Context

While the quiz runs, each player sees the current question on their phone and submits an answer. This is the moment-to-moment player surface.

## Acceptance criteria

- [ ] When the host advances, the question view updates on all connected players within the architecture latency budget (500ms on a healthy network).
- [ ] Question view shows: question text, four answer options (or text input for free-response), countdown timer.
- [ ] Player taps an answer. Submission is sent immediately. UI shows "submitted" state, disables further changes.
- [ ] Before submission, player can change their selection freely.
- [ ] After `ANSWER_REVEALED`, the player sees whether their answer was correct, the correct answer, their current score, and their team's current rank.
- [ ] Offline handling: if the player's network drops during a question, their pending submission is queued locally and sent on reconnect. If it arrives after reveal, show a non-blaming message ("your answer didn't arrive in time").
- [ ] Timer: client-side countdown for UX, server-side enforcement for correctness.
- [ ] Accessibility: WCAG AA, large-tap targets, screen-reader-friendly.
- [ ] Works on iOS Safari and Chrome on Android (min iOS 15, min Chrome 100).

## Files likely touched

- `webapp/src/features/quiz-player/`
  - `QuestionScreen.tsx` (new)
  - `AnswerFeedback.tsx` (new)
  - `PlayerLeaderboardCard.tsx` (new)
- `webapp/src/hooks/useQuizPlayerSession.ts` (extend from QUIZ-06)

## Dependencies

- Depends on: [QUIZ-01](../backend/QUIZ-01-session-service.md), [QUIZ-02](../backend/QUIZ-02-live-scoring-worker.md), [QUIZ-06](QUIZ-06-player-join-flow.md)

## Out of scope

- Showing the full room leaderboard (that is on the venue display).
- In-quiz chat or reactions.
- Multi-format question types beyond multiple choice and free text (v2).

## Notes

- Tap targets: minimum 48px square per platform guidance.
- Timer: trust the server timestamp in the event payload; do not rely on local clock.
- The "didn't arrive in time" copy matters. Make it sound like a system issue, not a player failure. UX has specific copy in the wireframes.
