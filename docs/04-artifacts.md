# 04. The artifact catalog

Every stage in CAIRN produces at least one artifact. This is the catalog: what each artifact is for, who owns it, how long it should be, and when to retire it.

Templates for each artifact live in [templates/](../templates/).

## The short list

If you only produce these, you have CAIRN:

1. **Problem statement**: what is wrong and for whom.
2. **Scope**: what you will and will not build this round.
3. **Architecture**: how the pieces fit.
4. **Story**: a single, implementable slice of work.
5. **QA checklist**: how you will know it is done.
6. **CLAUDE.md** (or equivalent): the AI context file.

The others below are valuable but optional.

## The full catalog

### Problem statement

- **Purpose.** Capture the problem worth solving, in plain language, without proposing a solution.
- **Owner.** Business Analyst (or Team Lead if no BA).
- **Size.** 200 to 500 words. If yours is longer, you are already solutioning.
- **When to write.** As the very first artifact in Discovery.
- **When to retire.** When the problem is solved and shipped. Archive, do not delete.
- **Anti-patterns.** Starting with "Users want a feature that..." That is not a problem, it is a proposed solution.

### Stakeholder interviews

- **Purpose.** Preserve the raw input from the people with the problem.
- **Owner.** Business Analyst.
- **Size.** One file per interview, structured but not polished.
- **When to write.** During Discovery.
- **When to retire.** Never. They are evidence. Compress into themes in `ux-research.md` but keep the originals.

### UX research

- **Purpose.** Turn observations into themes and opportunities.
- **Owner.** UX Designer/Researcher.
- **Size.** 1 to 3 pages.
- **When to write.** After interviews, before scope.
- **When to retire.** Archive after the feature ships.

### Scope

- **Purpose.** Draw the boundary around what you are building this round.
- **Owner.** Team Lead + BA.
- **Size.** One page. In-scope bullets, out-of-scope bullets, deferred bullets, rejected bullets.
- **When to write.** After research, before design.
- **When to retire.** Freeze when the Spec PR merges. Changes require a new Scope PR.
- **Anti-patterns.** A scope doc that only lists in-scope items. The out-of-scope list is where the doc earns its keep.

### Open questions

- **Purpose.** Track things you know you do not know, with owners and deadlines.
- **Owner.** Team Lead.
- **Size.** A table. Question, owner, deadline, status.
- **When to write.** Continuously, starting in Discovery.
- **When to retire.** Each question retires when answered. The file itself lives as long as the feature is active.

### Architecture

- **Purpose.** Describe how the pieces fit: services, boundaries, data flow, key decisions.
- **Owner.** Team Lead, with specialist input.
- **Size.** 2 to 5 pages. With a diagram.
- **When to write.** During Design.
- **When to retire.** Update as the system evolves. Do not let it rot.
- **Anti-patterns.** UML exhaustiveness. Nobody reads that. Show the shapes and the arrows and the decisions.

### Schema / data model

- **Purpose.** Describe the data, its relationships, its lifecycle.
- **Owner.** Backend lead or database specialist.
- **Size.** One page per aggregate. Diagrams help.
- **When to retire.** Update in the same PR as any migration.

### Story

- **Purpose.** Define a single unit of implementable work.
- **Owner.** Team Lead writes, Dev refines.
- **Size.** Half to one page. Context link, acceptance criteria, files likely touched, out-of-scope, notes.
- **When to write.** During Breakdown.
- **When to retire.** When the story is merged. Do not delete, leave it as an archive of what shipped and why.
- **Anti-patterns.** Stories that take more than three days. Stories that span platforms.

### QA checklist

- **Purpose.** Define how the team verifies a story is actually done.
- **Owner.** Team Lead, contributed to by everyone.
- **Size.** Short. Ten to fifteen items per feature is plenty.
- **When to write.** During Breakdown or before Release.
- **When to retire.** Feature-specific checklists archive with the feature. Repo-wide checklists (accessibility, security) live forever.

### Runbook

- **Purpose.** Tell an on-call engineer at 2am how to respond to an alert or recover from a failure.
- **Owner.** Whoever owns the service.
- **Size.** Per scenario, one page or less. Concrete commands.
- **When to write.** Before Release.
- **When to retire.** Update after every incident.

### CLAUDE.md (or .cursor/rules, or equivalent)

- **Purpose.** The top-level AI context file. Tells any AI session the repo's conventions, where to find things, and what it must never do.
- **Owner.** Team Lead.
- **Size.** Short. Hundreds of lines, not thousands. If it is too long, AI will ignore parts of it.
- **When to write.** Early in the project. Update when conventions change.
- **When to retire.** Never.
- **See.** [templates/CLAUDE.md.example](../templates/CLAUDE.md.example)

### Postmortem

- **Purpose.** After an incident, capture what happened, why, and what changes.
- **Owner.** Incident commander or Team Lead.
- **Size.** 1 to 3 pages.
- **When to write.** Within a week of the incident.
- **When to retire.** Never. They are corporate memory.

## The meta-rule

For any artifact you consider creating, ask:

1. **Who is going to read this?** If you cannot name them, do not write it.
2. **What decision does this support?** If none, do not write it.
3. **Could this be a paragraph in an existing artifact?** If yes, put it there instead of making a new file.

Every file in the repo has a cost. Pay it on purpose.
