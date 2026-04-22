# 04. The artifact catalog

Every stage in CAIRN produces at least one artifact. This is the catalog: what each artifact is for, who owns it, how long it should be, and how it ends.

Templates for each artifact live in [templates/](../templates/).

> All CAIRN artifacts live on the `cairn/<feature>` branch. None of them merge to `main`. They close with the long-lived Spec PR when the feature ships and stabilises. See [09-the-feature-branch-model.md](09-the-feature-branch-model.md).

## The short list

If you only produce these, you have CAIRN:

1. **Problem statement**: what is wrong and for whom.
2. **Scope**: what you will and will not build this round.
3. **Architecture**: how the new pieces fit, for this feature.
4. **Story**: a single, implementable slice of work.
5. **QA checklist**: how the team verifies the feature is done.

The others below are valuable but optional.

## The full catalog

### Problem statement

- **Purpose.** Capture the problem worth solving, in plain language, without proposing a solution.
- **Owner.** Business Analyst (or Team Lead if no BA).
- **Size.** 200 to 500 words. If yours is longer, you are already solutioning.
- **When to write.** As the very first artifact in Discovery.
- **End of life.** Closes with the Spec PR when the feature ships.
- **Anti-patterns.** Starting with "Users want a feature that..." That is not a problem, it is a proposed solution.

### Stakeholder interviews

- **Purpose.** Preserve the raw input from the people with the problem.
- **Owner.** Business Analyst.
- **Size.** One file per interview, structured but not polished.
- **When to write.** During Discovery.
- **End of life.** Closes with the Spec PR. The closed PR remains as the historical record.

### UX research

- **Purpose.** Turn observations into themes and opportunities.
- **Owner.** UX Designer/Researcher.
- **Size.** 1 to 3 pages.
- **When to write.** After interviews, before scope.
- **End of life.** Closes with the Spec PR.

### Scope

- **Purpose.** Draw the boundary around what you are building this round.
- **Owner.** Team Lead + BA.
- **Size.** One page. In-scope bullets, out-of-scope bullets, deferred bullets, rejected bullets.
- **When to write.** After research, before design.
- **End of life.** Closes with the Spec PR.
- **Anti-patterns.** A scope doc that only lists in-scope items. The out-of-scope list is where the doc earns its keep.

### Open questions

- **Purpose.** Track things you know you do not know, with owners and deadlines.
- **Owner.** Team Lead.
- **Size.** A table. Question, owner, deadline, status.
- **When to write.** Continuously, starting in Discovery.
- **End of life.** Each question retires when answered. The file closes with the Spec PR.

### Architecture

- **Purpose.** Describe how the new pieces fit, for this feature: components, boundaries, data flow, key decisions.
- **Owner.** Team Lead, with specialist input.
- **Size.** 2 to 5 pages. With a diagram.
- **When to write.** During Design.
- **End of life.** Closes with the Spec PR.
- **Anti-patterns.** UML exhaustiveness. Nobody reads that. Show the shapes and the arrows and the decisions. Do not try to describe the whole system; describe what is changing.

### Data model notes (feature-scoped)

- **Purpose.** Describe the data this feature introduces or changes.
- **Owner.** Backend lead or database specialist.
- **Size.** Short. Tables, fields, relationships.
- **When to write.** During Design, alongside architecture.
- **End of life.** Closes with the Spec PR. The migration in the codebase is the durable record.

### Story

- **Purpose.** Define a single unit of implementable work.
- **Owner.** Team Lead writes, Dev refines.
- **Size.** Half to one page. Context link, acceptance criteria, files likely touched, out-of-scope, notes.
- **When to write.** During Breakdown.
- **End of life.** Closes with the Spec PR. The shipped code is the durable record.
- **Anti-patterns.** Stories that take more than three days. Stories that span platforms.

### QA checklist

- **Purpose.** Define how the team verifies the feature is actually done.
- **Owner.** QA, contributed to by everyone.
- **Size.** Short. Ten to fifteen items per feature is plenty.
- **When to write.** During Breakdown or before Release.
- **End of life.** Closes with the Spec PR. The test suite in the codebase is the durable record.

### Spec PR description

- **Purpose.** Anchor the long-lived PR with a summary of what is being built and what reviewers should focus on.
- **Owner.** Team Lead.
- **Size.** Short. A few paragraphs and a checklist.
- **When to write.** When the Spec PR opens.
- **End of life.** The PR description remains forever on the closed PR.

## What is not in this catalog

CAIRN deliberately does not own:

- **System architecture** (the codebase as it currently stands).
- **Schema** as the live, deployed truth.
- **Conventions and standards.**
- **Runbooks.**
- **Project-level AI context files** (CLAUDE.md, .cursor/rules, etc.).
- **Postmortems and incident records.**

These are valuable artifacts. They are not feature-scoped. Whether and how your team maintains them is decided by your team or your company, not by CAIRN. If you have them, they live wherever your team has decided. CAIRN does not put them on the feature branch and does not put them on `main` either; that is your call.

If your team has none of these today, CAIRN does not require you to start. You can adopt CAIRN purely as feature-build scaffolding without changing anything else.

## The meta-rule

For any artifact you consider creating, ask:

1. **Who is going to read this?** If you cannot name them, do not write it.
2. **What decision does this support?** If none, do not write it.
3. **Could this be a paragraph in an existing artifact?** If yes, put it there instead of making a new file.

Every file on the feature branch has a cost. Pay it on purpose.
