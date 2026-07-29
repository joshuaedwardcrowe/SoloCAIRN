# SoloCAIRN: <feature name>

> Copy this into the PR description when opening an SoloCAIRN PR for a new feature.
>
> **In the separate-SoloCAIRN-repo model:** this is the PR introducing the new `features/<feature-slug>/` folder in the SoloCAIRN repo. It will merge into the SoloCAIRN repo's `main` (not the code repo's). Follow-on artifacts come in subsequent PRs.
>
> **In the long-lived branch model:** rename the title to `[SoloCAIRN] <feature> (do not merge)`. This is the long-lived PR from `cairn/<feature-slug>` to the code repo's `main`. It accumulates artifacts and is closed without merging when the feature ships.

## What this PR contains (or what the feature will contain over time)

- [ ] Problem statement
- [ ] Stakeholder interview notes (sanitised)
- [ ] UX research summary
- [ ] Scope
- [ ] Architecture
- [ ] Open questions
- [ ] Stories (per platform)
- [ ] QA checklist

## Summary

One paragraph on what we are proposing to build and why. Reviewers should be able to understand the shape from this paragraph alone.

## Key decisions to review

Name the two or three most important decisions in this spec. These are where review attention should focus.

1. ...
2. ...
3. ...

## Still unresolved

What is not yet decided. Open questions that should not block the next stage of work, with owners.

- ...
- ...

## What reviewers should check

- Does the problem match what you hear from your stakeholders?
- Does the scope match what we can realistically build?
- Does the architecture match the rest of the system?
- Are there edges we have missed?

## Stakeholders tagged

- @... for product review
- @... for architecture review
- @... for UX review

---

## Reviewer checklist

- [ ] Problem and scope are aligned
- [ ] Architecture respects the existing system
- [ ] Key decisions have stated alternatives and tradeoffs
- [ ] Open questions have owners
- [ ] Size is proportional to the work ahead
