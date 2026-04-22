# UX Research: Pub Quiz Live Scoring

## Linked artifacts

- Problem statement: [00-problem-statement.md](00-problem-statement.md)
- Stakeholder interviews: [01-stakeholder-interviews.md](01-stakeholder-interviews.md)
- Wireframes: `ux/` (external, not included in this example)

## Research method

- Eight host interviews over three weeks.
- Three venue manager interviews.
- Observation of three quiz nights (two gastropubs, one chain pub).
- A short survey via the hosts reached 50 players, 34 responses.
- Competitor scan of three adjacent products (QuizXR, SpeedQuiz, and a Kahoot education repurpose).

## Key themes

### Theme 1: Scoring is the friction, visibility is the opportunity

Hosts describe the marking pauses as the worst part of the evening. Players describe "not knowing where we stand" as their biggest frustration. These are two sides of the same coin: the current process hides state that everyone wants to see.

The implication is more than "automate scoring." It is "make the state of the quiz continuously visible." Real-time position after every question is not a nice-to-have; it is the point.

### Theme 2: The host is the product

Both players and venue managers talked about the host as the source of the good night. A good host can rescue a bad quiz; a bad host will ruin a good quiz. Any tool we build must amplify the host, not compete with them.

This rules out designs where the tech becomes centre stage. The host still runs the room.

### Theme 3: Phones are divisive at the table

Roughly half the players interviewed like the idea of using their phones. The other half actively dislike it ("phones kill the vibe"). Our product cannot require phones for everyone. It must let paper-and-phone coexist at the same table, scored under the same rules.

### Theme 4: Infrastructure is worse than we assumed

Five of eight hosts volunteered that wifi is a worry before we asked. Two venues have "big screens" that are in fact old smart TVs. Any design that assumes reliable realtime connections or HD-capable displays will break in the real world.

### Theme 5: Hosts vary more than players

Freelance hosts want deep customisation and their own content. Chain-venue hosts want a turnkey experience they cannot break. A single rigid tool will alienate one of these groups; we need to choose deliberately which we serve first.

## Current user journey

Today, a typical quiz night looks like:

1. Host arrives, sets up mic, distributes paper answer sheets.
2. Players arrive, form teams, fill in team name on sheet.
3. Host reads questions, players write answers.
4. After each round (6 to 10 questions), players pass sheets forward.
5. Host marks during a break (or has a volunteer mark).
6. Host announces running scores at the end of each round.
7. Repeat 3 to 6 for four rounds.
8. Final scores announced. Prize given.

## Opportunities

- **Automate scoring.** Eliminate the mid-quiz pauses.
- **Continuous visibility.** Show position after every question, not just after every round.
- **Fallback parity.** Let paper teams play alongside app teams without feeling second class.
- **Host-first tooling.** The console is the host's instrument. Build it for them.

## Risks and unknowns

- **Wifi.** If we depend on a good connection, the product will feel broken half the time.
- **Phone reluctance.** If we tilt the design toward phones, we alienate a meaningful segment.
- **Cheating.** With phones in hand, Googling is trivial. Addressing this at the policy level (time pressure, integrity culture) may be more practical than a technical fix.
- **Host trust.** A host embarrassed once by our tech will not come back.

## Recommendations

1. Treat the host console as the primary product surface. Invest design effort there first.
2. Design for intermittent connectivity from day one. Local-first where possible.
3. Make paper fallback trivial and visible in the UI for the host, so they can run a quiz even if the player side is down.
4. Do not solve cheating technically in v1. Time pressure and small-group social pressure are the real deterrents.
5. Serve the chain-venue host first (turnkey), then layer customisation for freelancers in a later round.
