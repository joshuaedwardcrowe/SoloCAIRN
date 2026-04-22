# Story: QUIZ-04 Host Console

## Context

The host console is the primary product surface. The host runs the whole quiz from here. It must be robust, calm, and fast. See [02-ux-research.md](../../02-ux-research.md) Theme 2.

See `ux/host-console/` for wireframes (external).

## Acceptance criteria

- [ ] Host can authenticate and create a new session from a pre-built quiz template.
- [ ] Host sees a "waiting room" view showing teams as they join.
- [ ] Host can start the quiz, advance to the next question, reveal the answer, pause, and end.
- [ ] Primary action button is always large, primary-coloured, and keyboard-accessible (spacebar advances).
- [ ] Live leaderboard visible in a side panel, non-distracting.
- [ ] Connection status indicator: green (WebSocket), yellow (fallback polling), red (disconnected, with reconnect).
- [ ] Paper-team management: host can add a paper team, submit scores per round.
- [ ] Responsive layout: works on laptop (primary), tablet (secondary). Phone is not a target.
- [ ] Loading, empty, error states for all views.
- [ ] Accessibility: WCAG AA, keyboard-navigable.

## Files likely touched

- `webapp/src/features/quiz-host/` (new directory)
  - `HostConsole.tsx`
  - `WaitingRoom.tsx`
  - `QuestionView.tsx`
  - `Leaderboard.tsx`
  - `ConnectionStatus.tsx`
  - `PaperTeams.tsx`
- `webapp/src/api/quiz.ts` (new, client for quiz endpoints)
- `webapp/src/hooks/useQuizSession.ts` (new, WebSocket + fallback logic)

## Dependencies

- Depends on: [QUIZ-01](../backend/QUIZ-01-session-service.md), [QUIZ-03](../backend/QUIZ-03-question-bank-api.md)

## Out of scope

- Venue display (QUIZ-05).
- Player flow (QUIZ-06, QUIZ-07).
- Host-authored quiz creation UI (v2).

## Notes

- Keyboard-first: hosts are busy. Spacebar advance is a research-validated convention.
- Connection status: research told us hosts worry about wifi. Make the state visible. Make recovery obvious.
- Avoid animations on the host console. The host does not want surprises.
