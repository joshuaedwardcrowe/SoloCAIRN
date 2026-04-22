# Architecture: <feature name>

> Copy this file to `features/<feature-slug>/architecture.md` in your CAIRN repo (or, in the branch model, the same path on the `cairn/<feature-slug>` branch).
> Aim for 2 to 5 pages. Include a diagram. If it is longer, it is probably trying to be a textbook.

## Linked artifacts

- Problem statement: `problem-statement.md`
- Scope: `scope.md`
- Existing architecture references: `docs/architecture.md` (project-wide)

## Overview

One paragraph. What are we adding, and how does it fit into the existing system?

## Diagram

```
<ASCII diagram or link to an exported SVG/PNG>
```

Show the components, the major data flows, and the boundaries. Do not show every class or function. Show shapes and arrows.

## Key decisions

Name the decisions that matter and why we made them. Future-you will thank current-you for writing these down.

### Decision 1: <title>

- **Choice.** What we picked.
- **Alternatives considered.** What we looked at and rejected.
- **Why this one.** The reasoning.
- **Tradeoffs we accept.** What we give up.

### Decision 2: <title>

...

## Components

For each new or significantly changed component:

### <Component name>

- **Responsibility.** What it does, in one sentence.
- **Interface.** Public API shape, or pointer to where it is defined.
- **Dependencies.** What it calls, what calls it.
- **Failure modes.** What happens when it fails.

## Data

- **New data.** Tables, fields, events introduced.
- **Changes to existing data.** Migrations, schema shifts.
- **Lifecycle.** Created when, updated by whom, retained for how long.

See `schema.md` for the full data model if it exists.

## External dependencies

Third-party services, libraries, or APIs this feature relies on. For each: what we use, why, and the cost of switching.

## Non-functional considerations

- **Performance.** Expected load, acceptable latency, anything to watch.
- **Security.** Sensitive data, authentication boundaries, new attack surface.
- **Observability.** Metrics, logs, alerts to add.
- **Accessibility.** If user-facing: explicit notes on WCAG level and key concerns.
- **Cost.** Noteworthy runtime costs.

## Rollout

How we plan to ship this safely. Feature flags, migrations, canary, dark launch.

## Open questions

| Question | Owner | Due |
|---|---|---|
| ... | ... | ... |

---

## Review checklist (for the PR)

- [ ] Diagram included
- [ ] Key decisions listed with alternatives and tradeoffs
- [ ] Failure modes described, not just happy path
- [ ] Data changes are explicit
- [ ] Non-functional concerns are addressed
- [ ] Rollout plan exists
