# 03. The SoloCAIRN lifecycle

A feature in SoloCAIRN moves through nine stages. Not every feature needs every stage. A bug fix might start at Build. A research spike might never leave Discovery. The lifecycle is a map, not a track you have to run.

```
Discovery → Research → Scope → Design → Breakdown → Build → Review → Release → Operate
                          ↑        ↑                    │       │
                          └────────┴────────────────────┴───────┘
                     revise Scope/Design when Build or Review reveals
                        something new — same feature, no new PR cycle
                                    required to "restart"

                 Operate ─────────────────────────────────────► Discovery
                        (learnings feed the *next* feature's Discovery)
```

The horizontal arrows are handoffs, always mediated by a reviewed artifact — but **SoloCAIRN treats these two loops as equally real, not just the outer one.** CAIRN (the methodology SoloCAIRN forks from) draws only the Operate→Discovery loop, which means learning only ever informs the *next* feature. That is too slow for a team trying to stay Agile: if Build or Review reveals that Scope or Design was wrong, the fix is a small, fast artifact-revision PR against *this* feature's Scope/Design, not a note for next time. See "Revising mid-flight," below.

### Revising mid-flight

Scope and Design being reviewed and merged does not freeze them. Approval means "good enough to act on now," not "correct forever." If Breakdown, Build, or Review surfaces something the earlier artifact got wrong or missed:

1. Open a small, fast PR against the affected artifact (`scope.md`, `architecture.md`, or the specific story) in the chosen SoloCAIRN location — same mechanics as any other SoloCAIRN PR, just smaller and faster than the original.
2. Get it reviewed by whoever owns that artifact's area (the same people who'd review it in its home stage — no need to re-run the whole stage).
3. Continue Build/Breakdown once it lands. Don't block on a full re-approval of everything downstream of the change unless the change actually invalidates other in-flight stories too.

This is the same discipline as any other SoloCAIRN artifact (written down, reviewed, in-repo) — it just runs on the timescale of "I hit this an hour ago," not "we'll note it for the retro."

## The nine stages

### 1. Discovery

**What happens.** Somebody (a customer, a stakeholder, a support ticket, a pattern in the data) surfaces a problem worth solving. You do not yet know what the solution looks like, or even whether it is worth building.

**Who leads.** The [Maintainer](../roles/maintainer.md), drawing on the [Business Analysis](../skills/business-analyst.md) skill.

**Artifacts produced.**
- `problem-statement.md`: what is wrong today, who is affected, what good looks like.
- `stakeholder-interviews.md`: notes from conversations with the people who have the pain.

**How AI helps.** Transcribes and summarises interviews. Drafts the problem statement from notes. Suggests questions the BA might have missed.

**How AI does not help.** It does not sit in the room. It does not notice body language. It does not decide what is worth investigating.

**Done when.** The team can answer, in one paragraph, what the problem is and who has it.

### 2. Research

**What happens.** You dig into how the problem shows up in real life. Users, flows, existing behaviour, competitive landscape. This is where UX and BA earn their keep.

**Who leads.** The [Maintainer](../roles/maintainer.md), drawing on the [UX Design / Research](../skills/ux-designer.md) and [Business Analysis](../skills/business-analyst.md) skills.

**Artifacts produced.**
- `ux-research.md`: observations, themes, opportunities.
- Optional: personas, journey maps, landscape notes.

**How AI helps.** Clusters interview notes into themes. Drafts journey maps from bullet points. Summarises competitor feature pages.

**How AI does not help.** It cannot watch a user struggle. It cannot empathise. It cannot notice the thing the user did not say.

**Done when.** The team has a shared mental model of the user's current experience and where the opportunity is.

### 3. Scope

**What happens.** You decide what you are actually going to build in this round. In-scope, out-of-scope, deferred, rejected. This is the moment where ambition meets reality.

**Who leads.** The [Maintainer](../roles/maintainer.md). Stakeholders (if any) approve.

**Artifacts produced.**
- `scope.md`: the decisions.
- `open-questions.md`: the things you still need to resolve, with owners.

**How AI helps.** Surfaces inconsistencies between scope and the research. Drafts the first cut of in/out lists from a conversation transcript.

**Done when.** A **Spec PR** is open in the chosen SoloCAIRN location (a separate SoloCAIRN repo or a long-lived branch in the code repo) containing problem, research, and scope. The PR is reviewed by the full team. Approval means "good enough to act on now" — not a freeze; see [Revising mid-flight](#revising-mid-flight) above. See [09-deployment-models.md](09-deployment-models.md) for where the artifacts live.

### 4. Design

**What happens.** The team decides how the system will work. Architecture, data model, API shapes, major UX patterns. This is a multi-role activity: UX, backend, frontend, mobile, and database thinking all converge.

**Who leads.** The [Maintainer](../roles/maintainer.md), drawing on [UX Design / Research](../skills/ux-designer.md) for UX patterns and whichever [Build skills](../skills/) the work will need.

**Artifacts produced.**
- `architecture.md`: how the pieces fit, with a diagram.
- `schema.md` or similar: data model.
- UX design references: wireframes, flows, design system notes.

**How AI helps.** Drafts architecture from requirements. Proposes data models. Spots inconsistencies between the design and the scope. Generates diagrams from descriptions.

**How AI does not help.** It does not know your existing system's quirks. Feed it your current architecture as context, or its suggestions will be generic.

**Done when.** The Spec PR (or a follow-up Spec PR) now includes design and has been re-reviewed. Same non-freeze rule as Scope: this is "good enough to start Breakdown/Build," and gets revised via a small follow-up PR (see [Revising mid-flight](#revising-mid-flight)) if reality disagrees with it.

### 5. Breakdown

**What happens.** The work gets sliced into stories. Each story is small enough to be built and reviewed in one go, and belongs to a single platform (backend, frontend, mobile, database).

**Sizing.** CAIRN sizes stories in time (ideally one to three days). SoloCAIRN treats that as one valid option, not the only one — **Fibonacci story points** are equally valid, and often the better fit for irregular/intermittent contribution: a time estimate silently assumes something like continuous engagement, and stops meaning anything if contribution is a scattered hour a week. A point captures effort, complexity, and risk together rather than just duration, and pairs with **velocity** — points completed per work session/cycle, tracked empirically rather than assumed — to absorb an irregular pace without needing every estimate redone. Pick whichever fits your actual contribution pattern; don't mix both within one project.

**Calibrating.** Points are relative, so your first estimation session has nothing to compare against. Rather than sizing items one at a time in isolation, order the batch against each other first, then anchor the scale by agreeing two reference items you understand well — say a two and a five. Two anchors rather than one matters: pinning everything to a single smallest item biases later estimates downward, and leaves nothing underneath it without resorting to fractions. From then on, estimate by **triangulation** — compare each new item against two already-estimated ones, ideally one smaller and one larger ("more than that three, less than that eight"). Working solo this carries more weight than it does for a team: there's no planning-poker round to surface a second opinion, so the reference items are the only thing standing between you and re-deriving the scale from scratch every session. Keep them somewhere visible during refinement.

**Re-estimating.** Re-estimate a story when its understood scope genuinely changes — you learn mid-build it's bigger or smaller than thought, so you revise the point value or split it (see [Revising mid-flight](#revising-mid-flight)). Don't re-estimate after the fact based on how long it actually took — that feeds velocity, an aggregate, forward-looking calibration, not a rewrite of one ticket's history. Stale, not-yet-started items can be re-sized during backlog grooming as your calibration matures; that's different from touching something already in flight or done.

**Who leads.** The [Maintainer](../roles/maintainer.md).

**Artifacts produced.**
- `features/<feature>/stories/backend/STORY-XX.md`
- `features/<feature>/stories/frontend/STORY-XX.md`
- `features/<feature>/stories/mobile/STORY-XX.md`
- `features/<feature>/stories/database/STORY-XX.md`

Each story follows the [story template](../templates/story.md).

**How AI helps.** Expands a scope bullet into a full story file with acceptance criteria. Proposes a reasonable slicing. Spots missing stories by cross-checking scope and architecture.

**Done when.** Stories are added to the chosen SoloCAIRN location through a reviewed PR. Devs push back on anything unclear; QA pushes back on missing edge cases, error states, and non-functional concerns. Approval means these stories are ready to pick up — not that the breakdown is final; splitting, re-ordering, or rewriting a story mid-Build is a normal small PR, not a process violation.

### 6. Build

**What happens.** Devs pick up stories and implement them. Each dev works in a branch, with AI as an accelerator. Because the story and all upstream artifacts are in the repo, every AI session starts with full context.

**Who leads.** The [Contributor](../roles/contributor.md) who picked up the story.

**Artifacts produced.** Code. Tests. Updated docs if the implementation revealed something the design missed.

**How AI helps.** Drafts code against the story. Writes tests for the acceptance criteria. Surfaces relevant existing code. Keeps the implementation consistent with repo conventions.

**Done when.** A **Code PR** is open, linked to its story, with acceptance criteria met.

### 7. Review

**What happens.** A teammate reviews the code PR against the story's acceptance criteria, the repo conventions, and general quality. QA verifies the feature against the QA checklist, often by running it. UX reviews for visual and interaction fidelity. These can happen in parallel.

**Who leads.** Whoever reviews (another [Contributor](../roles/contributor.md), or the [Maintainer](../roles/maintainer.md) self-reviewing after a real gap — see [Contributor: on review, honestly](../roles/contributor.md#on-review-honestly)) owns the review, drawing on the [QA](../skills/qa.md) skill for verification. The author owns the fixes.

**Artifacts produced.** Comments, suggestions, approvals. Bug reports for issues found. Occasionally a new story if scope leaked.

**How AI helps.** Drafts reviews. Spots things humans miss (missing null checks, accessibility gaps, test holes). Drafts test cases. Explains unfamiliar code.

**How AI does not help.** It cannot approve a PR. It cannot run the feature on a real device and feel whether it is right. Approval and verification are human decisions with accountability attached.

**Done when.** The PR is approved, the QA checklist is signed off, and the PR is merged.

### 8. Release

**What happens.** The feature ships, gradually or fully. Feature flags, canary rollouts, phased releases. The team watches for regressions.

**Who leads.** The [Maintainer](../roles/maintainer.md).

**SoloCAIRN artifacts produced.** Release notes drafted from the QA checklist and merged code PRs.

**Adjacent (not SoloCAIRN) artifacts your team may also produce.** Runbook updates, monitoring and alert configurations, system architecture deltas. These are project-level concerns; how they are handled is up to your team.

**How AI helps.** Drafts release notes from merged PRs and the QA checklist. Suggests metrics to watch.

**Done when.** The feature is in front of users at the intended exposure level.

### 9. Operate

**What happens.** The feature is live. It is being used, misused, and monitored. Bugs, edge cases, and surprising usage patterns surface. The team learns. Once the feature is stable, the SoloCAIRN artifacts are ended: the feature folder is archived (separate-repo model) or the long-lived branch PR is closed without merging (branch model). Either way, the code on `main` is the operational truth from now on; the SoloCAIRN history is the historical record.

**Who leads.** The [Maintainer](../roles/maintainer.md), with any active [Contributors](../roles/contributor.md) flagging what they hit.

**SoloCAIRN artifacts produced.** Updates to the open questions and QA checklist as reality teaches you something. New stories for any follow-ups handled within the same feature scope.

**Adjacent (not SoloCAIRN) artifacts your team may also produce.** Incident notes, postmortems, lessons-learned writeups. These belong wherever your team's project-level docs live.

**How AI helps.** Summarises logs. Searches the codebase for related code paths when debugging.

**Done when.** Never for the operational work. For SoloCAIRN: when the feature is stable, the artifacts end. In the separate-repo model that means the feature folder is archived or deleted. In the branch model that means the long-lived Spec PR is closed without merging.

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

SoloCAIRN distinguishes two kinds of work. The exact PR shapes depend on your chosen deployment model.

1. **SoloCAIRN PRs** land artifacts in your chosen SoloCAIRN location (a separate repo or a feature branch). Reviewed by the people whose work depends on the artifact. In a separate SoloCAIRN repo these merge to that repo's `main` normally. In the branch model they land on the feature branch via sub-PRs, and the long-lived branch PR against the code repo's `main` is never merged.
2. **Code PRs** are normal code PRs in the code repo from `feat/<story-id>` into `main`, the implementation of a single story. Reviewed against the story's acceptance criteria. The PR description links to the story file using an absolute URL when the artifacts live in a separate SoloCAIRN repo (filesystem-relative paths do not resolve cross-repo in web review UIs), or a normal in-repo URL when the artifacts live on a branch in the same repo.

See [09-deployment-models.md](09-deployment-models.md) for the full mechanics under each model.

If you find yourself wanting a third or fourth kind, you probably want a bigger version of one of these two.

### A note on the term "Spec PR"

Throughout these docs, **Spec PR** is shorthand for "the PR (or family of PRs) that lands an SoloCAIRN artifact for review." It refers to two structurally different things depending on your deployment model:

- **Separate-repo model (recommended)**: Spec PRs are normal short-lived PRs in the SoloCAIRN repo that merge into the SoloCAIRN repo's `main`. There can be many per feature, each landing one or a few artifacts.
- **Branch model**: there is a single long-lived Spec PR from `cairn/<feature>` to the code repo's `main` that **never merges**, plus optional small sub-PRs targeting the feature branch. The long-lived PR is closed without merging at the end of the feature.

When the docs say "the Spec PR closes" or "ends with the feature," translate accordingly: in the separate-repo model that means the feature folder is archived or deleted; in the branch model that means the long-lived PR is closed without merging.
