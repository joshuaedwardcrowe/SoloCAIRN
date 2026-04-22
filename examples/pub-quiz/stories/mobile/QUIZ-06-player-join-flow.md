# Story: QUIZ-06 Player Join Flow

## Context

Players join a quiz by scanning a QR code with their phone camera, landing on a URL that lets them join a team or create one. This is the player's first impression of the product.

Note: v1 is mobile-web, not native. See [04-architecture.md](../../04-architecture.md) §Key decisions 4.

## Acceptance criteria

- [ ] QR code encodes `https://<app-domain>/quiz/{session-code}`.
- [ ] Landing page asks: join existing team or create new team.
- [ ] Create: player enters a team name (max 30 chars, profanity filter). Gets a team token. Becomes team captain.
- [ ] Join: player picks an existing team from a list, joins without needing a code.
- [ ] After joining, the player lands on the waiting view: their team name, teammates joined so far, and a "ready when the host starts" message.
- [ ] Session code can also be entered manually on a fallback URL (`/quiz`) for players who cannot scan.
- [ ] Graceful degradation: if the player loses network, shows a "reconnecting" state; recovers automatically.
- [ ] Team token persisted in local storage so the player can close and reopen the tab without re-joining.
- [ ] Accessibility: WCAG AA, keyboard-navigable, screen-reader-friendly.

## Files likely touched

- `webapp/src/features/quiz-player/` (new directory)
  - `JoinScreen.tsx`
  - `TeamListScreen.tsx`
  - `CreateTeamScreen.tsx`
  - `WaitingRoom.tsx`
- `webapp/src/hooks/useQuizPlayerSession.ts` (new)
- `webapp/src/api/quiz-player.ts` (new)

## Dependencies

- Depends on: [QUIZ-01](../backend/QUIZ-01-session-service.md)

## Out of scope

- Answer submission UI (QUIZ-07).
- Native mobile apps.
- Team captain permissions or kick/ban features.

## Notes

- Mobile-first layout. Test on real phones (small Android, large iOS) before merging.
- Profanity filter: use existing `shared/profanity.ts` utility if present; otherwise a simple blocklist for v1.
- LocalStorage fallback for Safari private browsing: if unavailable, use sessionStorage and accept the limitation.
