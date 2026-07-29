# Example: Pub Quiz Live Scoring

This is a worked example of a feature going through ACAIRN end to end. It shows what the artifacts actually look like, in realistic detail, so you can see the method applied rather than described.

> In a real project, all artifacts shown here would live in the team's ACAIRN location: a separate ACAIRN repo (recommended) under `features/pub-quiz-live-scoring/`, or a long-lived `cairn/pub-quiz-live-scoring` branch in the code repo. They never reach the code repo's `main`. When the feature ships and stabilises, the folder is archived (or the branch PR is closed without merging). See [docs/09-deployment-models.md](../../docs/09-deployment-models.md) for the mechanics and the choice between them.

> This is example content. The product, the company, and the stakeholders are invented. Any resemblance to a real quiz platform is coincidental.

## The feature

A hosted pub-quiz experience for venues:

- The **host** runs a quiz session from a web console on their laptop or tablet.
- A **big screen** at the venue (the "venue display") shows questions and the live leaderboard.
- **Players** join on their phones by scanning a QR code, answer on their phones, and see their own score.

## What this example demonstrates

- The full set of feature-scoped artifacts a team would produce, sliced across backend, frontend, mobile, and database.
- A **QA checklist** that ties every story's acceptance criteria to a feature-level verification gate.
- Cross-role handoffs, with each artifact produced by the right role.
- Pragmatic compromises and open questions kept visible instead of hidden.

When the feature ships and stabilises, the team would archive these artifacts (or close the long-lived branch PR, depending on the deployment model). The code repo's `main` never sees them.

## The artifacts (all in the ACAIRN location)

### Spec artifacts

- [00-problem-statement.md](00-problem-statement.md)
- [01-stakeholder-interviews.md](01-stakeholder-interviews.md)
- [02-ux-research.md](02-ux-research.md)
- [03-scope.md](03-scope.md)
- [04-architecture.md](04-architecture.md)
- [05-open-questions.md](05-open-questions.md)

### QA artifacts

- [06-qa-checklist.md](06-qa-checklist.md)

### Stories

- [stories/backend/](stories/backend/)
  - [QUIZ-01-session-service.md](stories/backend/QUIZ-01-session-service.md)
  - [QUIZ-02-live-scoring-worker.md](stories/backend/QUIZ-02-live-scoring-worker.md)
  - [QUIZ-03-question-bank-api.md](stories/backend/QUIZ-03-question-bank-api.md)
- [stories/frontend/](stories/frontend/)
  - [QUIZ-04-host-console.md](stories/frontend/QUIZ-04-host-console.md)
  - [QUIZ-05-venue-display.md](stories/frontend/QUIZ-05-venue-display.md)
- [stories/mobile/](stories/mobile/)
  - [QUIZ-06-player-join-flow.md](stories/mobile/QUIZ-06-player-join-flow.md)
  - [QUIZ-07-player-answer-ui.md](stories/mobile/QUIZ-07-player-answer-ui.md)
- [stories/database/](stories/database/)
  - [QUIZ-08-schema.md](stories/database/QUIZ-08-schema.md)

## How to read it

1. Start with [00-problem-statement.md](00-problem-statement.md). Notice how it stays out of solution mode.
2. Skim [01-stakeholder-interviews.md](01-stakeholder-interviews.md) for the raw input.
3. Read [02-ux-research.md](02-ux-research.md) to see how the interviews become themes.
4. Read [03-scope.md](03-scope.md) to see the decisions.
5. Read [04-architecture.md](04-architecture.md) to see the design.
6. Skim the stories under `stories/` to see how a team would slice this into week-sized chunks.
7. Read [06-qa-checklist.md](06-qa-checklist.md) to see how QA turns the design and stories into a verification gate.

The point is not to admire the example. The point is to notice what each artifact is doing, and to be able to produce similar shapes for your own features.
