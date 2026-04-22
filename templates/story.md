# Story: <STORY-ID> <short title>

> Copy to `features/<feature>/stories/<platform>/<STORY-ID>-<slug>.md`.
> Keep it to half a page or one page. If it grows, your story is too big.

## Context

One or two sentences on why this story exists. Link to the design it belongs to.

See `docs/features/<feature>/architecture.md` and `docs/features/<feature>/scope.md`.

## Acceptance criteria

The conditions that must hold for this story to be "done." Each should be testable.

- [ ] ...
- [ ] ...
- [ ] ...

## Files likely touched

A rough list. Not a contract, just a starting point.

- `path/to/file-a.ext` (new)
- `path/to/file-b.ext` (change)

## Dependencies

Stories that must land before this one, if any.

- Depends on: `STORY-XX`

## Out of scope

Things that might look related but are not this story's job.

- ...
- ...

## Notes

Anything else the implementer needs. Edge cases, constraints, non-obvious decisions.

- ...

---

## Definition of done (checklist for the code PR)

- [ ] All acceptance criteria met
- [ ] Tests added or updated
- [ ] Docs updated if behaviour or contracts changed
- [ ] No new TODOs or tech-debt shortcuts without tickets
- [ ] Reviewer has verified, not just read
