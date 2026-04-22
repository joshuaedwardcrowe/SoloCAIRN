# 03. The CAIRN lifecycle

A feature in CAIRN moves through nine stages. Not every feature needs every stage. A bug fix might start at Build. A research spike might never leave Discovery. The lifecycle is a map, not a track you have to run.

```
                    ┌──────────────────────────────────────────┐
                    │                                          │
   Discovery ──► Research ──► Scope ──► Design ──► Breakdown   │
                                                      │        │
                                                      ▼        │
                         Operate ◄── Release ◄── Review ◄── Build
                                                      ▲
                                                      │ (learnings feed back)
```

The horizontal arrows are handoffs, always mediated by a reviewed artifact. The feedback loop from Operate back into Discovery is where real learning lives.

## The nine stages

### 1. Discovery

**What happens.** Somebody (a customer, a stakeholder, a support ticket, a pattern in the data) surfaces a problem worth solving. You do not yet know what the solution looks like, or even whether it is worth building.

**Who leads.** Team Lead + Business Analyst.

**Artifacts produced.**
- `problem-statement.md`: what is wrong today, who is affected, what good looks like.
- `stakeholder-interviews.md`: notes from conversations with the people who have the pain.

**How AI helps.** Transcribes and summarises interviews. Drafts the problem statement from notes. Suggests questions the BA might have missed.

**How AI does not help.** It does not sit in the room. It does not notice body language. It does not decide what is worth investigating.

**Done when.** The team can answer, in one paragraph, what the problem is and who has it.

### 2. Research

**What happens.** You dig into how the problem shows up in real life. Users, flows, existing behaviour, competitive landscape. This is where UX and BA earn their keep.

**Who leads.** UX Designer/Researcher + Business Analyst.

**Artifacts produced.**
- `ux-research.md`: observations, themes, opportunities.
- Optional: personas, journey maps, landscape notes.

**How AI helps.** Clusters interview notes into themes. Drafts journey maps from bullet points. Summarises competitor feature pages.

**How AI does not help.** It cannot watch a user struggle. It cannot empathise. It cannot notice the thing the user did not say.

**Done when.** The team has a shared mental model of the user's current experience and where the opportunity is.

### 3. Scope

**What happens.** You decide what you are actually going to build in this round. In-scope, out-of-scope, deferred, rejected. This is the moment where ambition meets reality.

**Who leads.** Team Lead + Business Analyst. Stakeholders approve.

**Artifacts produced.**
- `scope.md`: the decisions.
- `open-questions.md`: the things you still need to resolve, with owners.

**How AI helps.** Surfaces inconsistencies between scope and the research. Drafts the first cut of in/out lists from a conversation transcript.

**Done when.** A **Spec PR** is open in the chosen CAIRN location (a separate CAIRN repo or a long-lived branch in the code repo) containing problem, research, and scope. The PR is reviewed by the full team. Approval is the gate. See [09-deployment-models.md](09-deployment-models.md) for where the artifacts live.

### 4. Design

**What happens.** The team decides how the system will work. Architecture, data model, API shapes, major UX patterns. This is a multi-role activity: UX, backend, frontend, mobile, and database thinking all converge.

**Who leads.** Team Lead facilitates. Each specialist contributes to their area.

**Artifacts produced.**
- `architecture.md`: how the pieces fit, with a diagram.
- `schema.md` or similar: data model.
- UX design references: wireframes, flows, design system notes.

**How AI helps.** Drafts architecture from requirements. Proposes data models. Spots inconsistencies between the design and the scope. Generates diagrams from descriptions.

**How AI does not help.** It does not know your existing system's quirks. Feed it your current architecture as context, or its suggestions will be generic.

**Done when.** The Spec PR (or a follow-up Spec PR) now includes design and has been re-reviewed.

### 5. Breakdown

**What happens.** The work gets sliced into stories. Each story is small enough to be built and reviewed in one go (ideally one to three days of work), and belongs to a single platform (backend, frontend, mobile, database).

**Who leads.** Team Lead (in a scrum-master role).

**Artifacts produced.**
- `features/<feature>/stories/backend/STORY-XX.md`
- `features/<feature>/stories/frontend/STORY-XX.md`
- `features/<feature>/stories/mobile/STORY-XX.md`
- `features/<feature>/stories/database/STORY-XX.md`

Each story follows the [story template](../templates/story.md).

**How AI helps.** Expands a scope bullet into a full story file with acceptance criteria. Proposes a reasonable slicing. Spots missing stories by cross-checking scope and architecture.

**Done when.** Stories are added to the chosen CAIRN location through a reviewed PR. Devs push back on anything unclear; QA pushes back on missing edge cases, error states, and non-functional concerns. Approval is the gate.

### 6. Build

**What happens.** Devs pick up stories and implement them. Each dev works in a branch, with AI as an accelerator. Because the story and all upstream artifacts are in the repo, every AI session starts with full context.

**Who leads.** The individual developer owns their story.

**Artifacts produced.** Code. Tests. Updated docs if the implementation revealed something the design missed.

**How AI helps.** Drafts code against the story. Writes tests for the acceptance criteria. Surfaces relevant existing code. Keeps the implementation consistent with repo conventions.

**Done when.** A **Code PR** is open, linked to its story, with acceptance criteria met.

### 7. Review

**What happens.** A teammate reviews the code PR against the story's acceptance criteria, the repo conventions, and general quality. QA verifies the feature against the QA checklist, often by running it. UX reviews for visual and interaction fidelity. These can happen in parallel.

**Who leads.** The code reviewer owns the code review. QA owns the verification against the checklist. The author owns the fixes.

**Artifacts produced.** Comments, suggestions, approvals. Bug reports for issues found. Occasionally a new story if scope leaked.

**How AI helps.** Drafts reviews. Spots things humans miss (missing null checks, accessibility gaps, test holes). Drafts test cases. Explains unfamiliar code.

**How AI does not help.** It cannot approve a PR. It cannot run the feature on a real device and feel whether it is right. Approval and verification are human decisions with accountability attached.

**Done when.** The PR is approved, the QA checklist is signed off, and the PR is merged.

### 8. Release

**What happens.** The feature ships, gradually or fully. Feature flags, canary rollouts, phased releases. The team watches for regressions.

**Who leads.** Team Lead or whoever owns release management.

**CAIRN artifacts produced.** Release notes drafted from the QA checklist and merged code PRs.

**Adjacent (not CAIRN) artifacts your team may also produce.** Runbook updates, monitoring and alert configurations, system architecture deltas. These are project-level concerns; how they are handled is up to your team.

**How AI helps.** Drafts release notes from merged PRs and the QA checklist. Suggests metrics to watch.

**Done when.** The feature is in front of users at the intended exposure level.

### 9. Operate

**What happens.** The feature is live. It is being used, misused, and monitored. Bugs, edge cases, and surprising usage patterns surface. The team learns. Once the feature is stable, the long-lived Spec PR is closed without merging; the closed PR remains as the historical record.

**Who leads.** The whole team, with the Team Lead coordinating.

**CAIRN artifacts produced.** Updates to the open questions and QA checklist as reality teaches you something. New stories for any follow-ups handled within the same feature scope.

**Adjacent (not CAIRN) artifacts your team may also produce.** Incident notes, postmortems, lessons-learned writeups. These belong wherever your team's project-level docs live.

**How AI helps.** Summarises logs. Searches the codebase for related code paths when debugging.

**Done when.** Never for the operational work. For CAIRN: when the feature is stable, the Spec PR is closed without merging.

## Which stages for which work

| Type of work | Stages you actually need |
|---|---|
| New feature (non-trivial) | All nine |
| Small enhancement | Scope → Design → Breakdown → Build → Review → Release |
| Bug fix | Story (optional) → Build → Review → Release |
| Research spike | Discovery → Research, then stop and decide |
| Technical debt | Scope → Design → Breakdown → Build → Review (often no Release doc needed) |
| Emergency hotfix | Build → Review → Release, then retrospectively write it up |

## The kinds of PR

CAIRN distinguishes two kinds of work. The exact PR shapes depend on your chosen deployment model.

1. **CAIRN PRs** land artifacts in your chosen CAIRN location (a separate repo or a feature branch). Reviewed by the people whose work depends on the artifact. In a separate CAIRN repo these merge to that repo's `main` normally. In the branch model they land on the feature branch via sub-PRs, and the long-lived branch PR against the code repo's `main` is never merged.
2. **Code PRs** are normal code PRs in the code repo from `feat/<story-id>` into `main`, the implementation of a single story. Reviewed against the story's acceptance criteria. Link to the story file by path or URL.

See [09-deployment-models.md](09-deployment-models.md) for the full mechanics under each model.

If you find yourself wanting a third or fourth kind, you probably want a bigger version of one of these two.
