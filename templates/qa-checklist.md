# QA Checklist: <feature name>

> Copy to `docs/features/<feature-slug>/qa-checklist.md`.
> Keep it short. Ten to fifteen items is plenty for most features.

A feature-specific checklist. Repo-wide concerns (security, accessibility baselines) belong in a shared checklist at `docs/checklists/`.

## Functional

- [ ] Happy path works end to end
- [ ] Each acceptance criterion from each story is verified in isolation
- [ ] Primary error paths display sensible messages

## Data

- [ ] No data leakage across tenants or users
- [ ] New fields are populated correctly on create and update
- [ ] Deletion or archival behaves as intended

## Edges

- [ ] Empty state is handled
- [ ] Very large inputs are handled
- [ ] Concurrent actions do not corrupt state
- [ ] Offline or degraded network is handled where applicable (mobile, web)

## UX

- [ ] Loading, empty, error, and success states all exist
- [ ] Keyboard navigation works on web
- [ ] Screen reader announces the key elements correctly
- [ ] Copy is in the right voice and correctly translated where applicable

## Performance

- [ ] No obvious regressions in key metrics
- [ ] Large datasets do not block the UI

## Observability

- [ ] Relevant metrics, logs, and alerts are in place
- [ ] A runbook exists for the top two failure modes

## Release

- [ ] Feature flag strategy is documented
- [ ] Rollback is documented
- [ ] Stakeholders know it is shipping

---

Use this as a starting point. Delete what does not apply. Add what does.
