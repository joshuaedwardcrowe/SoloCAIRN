# Scope: Pub Quiz Live Scoring

## Linked artifacts

- Problem statement: [00-problem-statement.md](00-problem-statement.md)
- UX research: [02-ux-research.md](02-ux-research.md)
- Architecture: [04-architecture.md](04-architecture.md)

## In scope

- **Host console (web).** A browser-based console the host runs on a laptop or tablet, to control a live quiz session: start, show next question, reveal answer, pause, end.
- **Venue display (web).** A browser-based full-screen view optimised for a TV, showing the current question, a timer, and the live leaderboard.
- **Player mobile app.** Players scan a QR code to join a session, submit answers, and see their team's score.
- **Real-time scoring.** Answers scored automatically. Leaderboard updates after each question.
- **Pre-built question bank.** A library of 500 questions across 10 categories, available to all hosts.
- **Paper fallback.** A host can mark a team as "paper" and submit their round scores manually.
- **Offline-tolerant player flow.** Players who lose signal briefly can rejoin without losing their score.
- **Session lifecycle.** Host creates session, players join, quiz runs, leaderboard closes, data persists for 30 days.

## Out of scope

- Host-authored custom questions (using only the pre-built bank in v1).
- Multi-venue simultaneous sessions.
- Leagues, championships, or ongoing player accounts across sessions.
- Payment, subscription, or monetisation flows.
- Audio/video reading of questions (text-only in v1).
- Native mobile apps (mobile is a mobile-optimised web app in v1; native deferred).
- Anti-cheat (beyond question timers).
- Accessibility beyond WCAG AA baseline (no specific screen reader choreography for the venue display in v1).

## Deferred

- Host-authored questions: next round, targets Q3.
- Native mobile apps: evaluate after v1 based on retention data.
- League mode: speculative, depends on traction.

## Rejected

- Voice-based answer submission: complexity does not match the value.
- Proprietary venue hardware (tablets, big screens): violates the "venues won't buy hardware" constraint from research.
- Anti-Google features (lockdown browser, proctoring): out of spirit with a pub quiz.

## Assumptions

- Venues have at least one screen we can cast to (TV, projector, large monitor).
- Hosts will bring their own laptop or tablet.
- Wifi is present but can be unreliable. Players may have cellular fallback.
- Quiz sessions are 60 to 120 minutes with 30 to 60 questions.
- Team sizes are 1 to 8 players. 50 teams per venue is the upper end.

## Success criteria

- In closed pilot at three venues: zero quiz nights abandoned due to tool failure.
- In pilot: 80% of teams complete the quiz without a reconnection error visible to the player.
- Hosts in post-pilot interviews would use it again.
- Median time from host "next question" to question visible on all surfaces under 1 second on a healthy network.
- Leaderboard visible on the venue display at all times except during question reveal transitions.

## Open questions

See [05-open-questions.md](05-open-questions.md).
