# Story: QUIZ-05 Venue Display

## Context

The venue display is the big screen in the pub. It shows what everyone is reading: the question, timer, and leaderboard. It must be readable across a noisy room.

## Acceptance criteria

- [ ] Opened at a session-specific URL (`/display/{code}`) that auto-connects.
- [ ] Full-screen layout optimised for a 1080p TV at 3 to 5 metres of viewing distance.
- [ ] Question view: question text large, timer prominent, current question number visible.
- [ ] Leaderboard view: top 10 teams with scores, updates smoothly.
- [ ] Transitions between question and leaderboard are simple and slow enough to follow.
- [ ] Connection status indicator in a corner; unobtrusive but always visible.
- [ ] Reconnects automatically on transient connection loss.
- [ ] Accessible: text contrast ratio >= 7:1 for readability across a room. This is above WCAG AAA; it is a legibility requirement, not an accessibility one.

## Files likely touched

- `webapp/src/features/quiz-display/` (new directory)
  - `VenueDisplay.tsx`
  - `QuestionView.tsx`
  - `LeaderboardView.tsx`
  - `TransitionLayer.tsx`
- `webapp/src/styles/quiz-display.css` (new)

## Dependencies

- Depends on: [QUIZ-01](../backend/QUIZ-01-session-service.md)

## Out of scope

- Remote-controlled scene transitions from the host console (v2).
- Multiple display layouts per venue (v2).
- Branding per venue (v2).

## Notes

- This is the only surface where we deliberately size type huge. Use a dedicated type scale, not the default design tokens.
- Leaderboard updates: animate position changes so viewers can follow teams moving up and down.
- No interactive controls on this view. It is view-only.
