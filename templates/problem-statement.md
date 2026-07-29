# Problem Statement: <feature name>

> Copy this file to `features/<feature-slug>/problem-statement.md` in your SoloCAIRN repo (or, in the branch model, the same path on the `cairn/<feature-slug>` branch).
> Aim for 200 to 500 words. If it grows longer, you are already proposing a solution.

## What is wrong today

Describe the current situation in plain language. What is happening, or not happening, that should not be?

Avoid solution language ("users need a bulk upload button"). Stick to observations ("users currently sign one document at a time, which takes too long when they have many documents to process").

## Who is affected

Which users, teams, or stakeholder groups are hurt by this today? How much? How often?

Concrete over abstract. "HR admins processing onboarding for new starters" beats "enterprise users."

## Evidence

Where is the pain visible? Support tickets, stakeholder interviews, usage data, churn signals.

- Stakeholder interview: see `stakeholder-interviews.md#admin-team`
- Support tickets: N tickets in the last quarter tagged as `slow-signing`
- Usage data: median time to sign a batch is X minutes

## What "solved" looks like

Describe the state of the world you are trying to reach. Still no solutioning. Focus on outcomes.

- Admins can process a batch of documents in under X minutes.
- Errors in a batch do not block the rest of the batch.
- Admins have confidence the batch completed correctly.

## Out of scope for this problem

What related problems are you explicitly not trying to solve here? This protects the scope of the work that will follow.

## Open questions

Questions that affect the problem itself, not yet the solution.

- Is this pain equally felt across customer segments?
- Is the volume trending up or down?

## Not yet decided

If the team has not yet agreed this problem is worth solving, say so. Problem statements can land in the SoloCAIRN location without commitment to build. The Scope artifact is where the commitment lives.

---

## Review checklist (for the PR)

- [ ] No solution language
- [ ] Affected users are named concretely
- [ ] Evidence is cited, not asserted
- [ ] Success is described as outcomes, not features
- [ ] Length under 500 words
