# Role: QA Engineer

You are the person who keeps the team honest about whether a feature actually works. In CAIRN, you are involved from the Story PR onwards, not bolted on at the end. Your artifacts are how the team agrees on what "done" really means.

## Who you are

- You think about what could go wrong, not just what should go right.
- You care about the user's experience under stress: bad networks, bad inputs, bad timing.
- You ask the questions that make developers uncomfortable in a useful way.
- You know the difference between testing a checkbox and testing a feature.

## Artifacts you own

- `qa-checklist.md` per feature: the verified-by-a-human list.
- Project-wide checklists in `docs/checklists/` (accessibility, security baseline, performance baseline).
- Test plans, where they exist as separate documents.
- Bug reports, structured and reproducible.

## Artifacts you contribute to

- Stories: you add acceptance criteria during the Story PR, especially around edges, error states, and non-functional concerns.
- `architecture.md`: you push back when the design is hard to test or makes failure modes invisible.
- `ux-research.md`: you flag where research found edge cases that need explicit test coverage.
- Code PRs: you review for testability and verify the feature, not just the code.

## How AI fits your work

- **Drafting test cases from acceptance criteria.** Hand AI a story file; ask for test cases. You curate, prune, and add the ones it missed.
- **Generating test data.** Realistic but anonymised data, edge cases, large datasets. AI is good at this.
- **Exploratory test ideas.** "Given this feature, what are 20 things that could go wrong?" Useful starting list.
- **Bug report drafting.** Symptoms-to-structured-report. You verify reproduction steps.
- **Regression sweep prompts.** "What existing flows might this change affect?" AI is good at surfacing related code paths from the repo.
- **Test code drafting.** First-pass automated tests against well-specified stories.

## How AI does not help

- It does not sit with the feature. Exploratory testing is a human craft.
- It does not notice the unexpected. The valuable bugs are often the ones nobody predicted.
- It will invent acceptance criteria during testing if you let it. Push back. The criteria are decided in the Story PR, not by the AI.
- It does not feel friction. UI that is "technically functional" but awful to use is a bug; AI rarely flags this.
- It cannot reproduce intermittent issues. Flakiness investigation is still your job.

## Anti-patterns for this role

- **Bolted-on QA.** Showing up only at the end of a sprint to "sign off." If your first contact with a feature is the Code PR, you are too late.
- **Test theatre.** A green dashboard does not mean the feature works. A passing checklist with no real exploration is theatre.
- **Bug bouncing.** "Could not reproduce, closing." Reproduce or escalate; do not silently close.
- **Owning quality alone.** Quality is a team responsibility. Your role is to lead and verify, not to be the only person who cares.
- **Letting AI sign off.** A test pass from AI is input to your decision, not the decision.

## A day in the life

**09:00.** Review the open Story PR. Add acceptance criteria for two stories: a missing offline state on mobile, an empty-state behaviour on the venue display. Comment with reasoning.

**10:00.** Pair with a backend dev on QUIZ-02 (live scoring worker). Walk through the test plan together. Identify two edge cases the unit tests do not cover; agree the dev will add them.

**11:30.** Review a Code PR for QUIZ-06. Pull the branch locally. Test on a real Android phone and an iPhone. Notice that the team-name input has a misaligned keyboard on iOS. File a structured bug; link it to the PR.

**14:00.** Update `docs/features/pub-quiz/qa-checklist.md` with the items the team agreed during the Story PR review.

**15:00.** Run an exploratory test session against the staging environment. Try things the team did not predict: rapid join-leave-join, joining a session that has already ended, scanning a stale QR code. Document what breaks.

**16:30.** Write up findings in the Code PR comments and the bug tracker. Two issues need to be addressed before merge; one is a follow-up story for v1.1.

**17:00.** Sign off on the QA checklist for QUIZ-04, which has cleared review and exploratory testing.

## The hidden job

Your hidden job is to keep the team's standard for "done" honest. Velocity pressures will always push toward calling things done sooner. You are the counterweight. Your authority is the artifact (the checklist, the bug report, the test plan), not your title. When the artifact says it is not done, it is not done. That clarity is the gift you give the team.
