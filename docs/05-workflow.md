# 05. The workflow

This is what a week inside CAIRN actually looks like. If the rest of the docs describe the shape, this one describes the motion.

## The PRs, in motion

CAIRN distinguishes a long-lived Spec PR (which never merges) and the code PRs that ship the work (which do merge). Knowing which one you are in at any moment is most of the discipline. See [09-the-feature-branch-model.md](09-the-feature-branch-model.md) for the full mechanics.

### Spec PR (long-lived, never merged)

**Branch name.** `cairn/<feature-slug>`

**Contains.** All CAIRN artifacts for this feature: problem, research, scope, architecture, stories, QA checklist, open questions. Docs only. No code.

**Lifetime.** Weeks to months. Opened at the start of the feature, accumulates artifacts as the work progresses, **closed without merging** when the feature ships and stabilises.

**Reviewers.** The full team. Everyone who will implement it has a say before implementation starts.

**Approval criteria.** The team agrees this is what we are building and roughly how. Open questions are listed but not all resolved. The PR remains open and is iterated on.

**What it looks like.**

```
cairn/pub-quiz-live-scoring (branch)
├── docs/features/pub-quiz/
│   ├── problem-statement.md
│   ├── stakeholder-interviews.md (sanitised)
│   ├── ux-research.md
│   ├── scope.md
│   ├── architecture.md
│   ├── open-questions.md
│   └── qa-checklist.md
└── tasks/pub-quiz/
    ├── backend/
    │   ├── QUIZ-01-session-service.md
    │   └── QUIZ-02-live-scoring-worker.md
    ├── frontend/
    │   └── QUIZ-03-host-console.md
    └── mobile/
        └── QUIZ-04-player-app-join-flow.md
```

### Sub-PRs against the feature branch

Artifacts can be reviewed individually or in batches via small PRs that target the `cairn/<feature>` branch (not `main`). For example:

- `spec/pub-quiz-architecture` → `cairn/pub-quiz-live-scoring`: lands the architecture doc.
- `stories/pub-quiz-backend` → `cairn/pub-quiz-live-scoring`: lands the backend stories.

These do merge, but only into the feature branch. Use them when you want clean, focused review on one artifact at a time.

### Code PR

**Branch name.** `feat/<story-id>-<short-description>`

**Branched from.** `main`

**Contains.** The implementation of exactly one story.

**Lifetime.** One to three days, ideally.

**Reviewers.** One or two teammates. At least one should know the area.

**Merge criteria.** Acceptance criteria met. Tests pass. Review approved. The relevant QA checklist item ticked. **Merges into `main`.**

**Linking.** PR description references the story file by URL on the `cairn/<feature>` branch. Devs needing the artifacts in their local workspace use a worktree or a sparse checkout of the feature branch (see [09-the-feature-branch-model.md](09-the-feature-branch-model.md)).

## A day in the life, by role

### Team Lead (Monday)

- 09:00. Open the Spec PR for the new feature. Paste in the problem statement draft. Tag stakeholders for review.
- 10:30. Review yesterday's sub-PR adding stories to the feature branch. Approve two stories, request changes on one (too big, needs splitting).
- 13:00. Pair with the BA on stakeholder interview notes. Draft the themes section of `ux-research.md`.
- 15:00. Review an open Code PR against its story. Acceptance criteria checked, two suggestions left, approve.
- 17:00. Update `open-questions.md` with answers from today's stakeholder call.

### Business Analyst (Tuesday)

- 09:00. Two stakeholder interviews back to back. Record both (with permission). Take sparse notes.
- 11:30. Feed transcripts to AI, get a themed summary. Clean it up into `stakeholder-interviews.md`.
- 14:00. Spot a contradiction between two stakeholders. Add to `open-questions.md` with yourself as owner.
- 15:30. Pair with UX to translate pain points into research themes.
- 17:00. Push a commit to the Spec PR branch. Comment on what changed.

### UX Designer (Wednesday)

- 09:00. Sketch the two key flows on paper.
- 11:00. Convert to wireframes in the design tool. Export to the repo as images under `docs/features/<feature>/ux/`.
- 13:00. Write a short `ux-research.md` that links to the wireframes and explains the design intent.
- 15:00. Review the mobile team's story drafts for interaction fidelity. Suggest two missing acceptance criteria.

### Backend Dev (Thursday)

- 09:00. Pick up story `QUIZ-01-session-service.md`. Branch: `feat/quiz-01-session-service`.
- 09:15. Start an AI session. The AI has access to the architecture doc and the story via a worktree of `cairn/<feature>`. Prompt: "Implement QUIZ-01 per the story file. Show me the plan first."
- 09:30. Review the plan. Push back on one part (the retry strategy is wrong for this use case). AI re-plans.
- 10:00. Implement, with tests, iteratively.
- 14:00. Story's acceptance criteria checked. Open Code PR. Link to story in description.
- 15:30. Address a review comment. Push the fix.
- 17:00. PR approved and merged.

### Mobile Dev (Friday)

- 09:00. Story `QUIZ-04-player-app-join-flow.md`. Branch off main.
- 09:30. AI session primed with the repo's mobile conventions, the relevant UX wireframe, and the story. Implement the QR scan + join screen.
- 12:00. Hit an ambiguity: the story says "graceful failure" but does not specify retry behaviour. Push an update to the story file on the `cairn/<feature>` branch as a note for future readers, then make a judgment call. Flag it in the Code PR description so the reviewer can weigh in.
- 15:00. PR open. Review requested from backend dev and UX.

### Frontend Dev (any day, similar shape)

The same pattern: pick a story, branch, AI-assisted implement, open Code PR, review.

### QA Engineer (across the week)

- Monday morning. Review the open Spec PR (specifically the new stories that landed there). Add acceptance criteria for two stories (an empty state, an offline behaviour). Comment with reasoning so devs see the why.
- Mid-week. Pair with backend dev on the test plan for a tricky story. Identify two edge cases the unit tests would miss; agree how to cover them.
- Wednesday afternoon. Pull a Code PR branch locally. Test on real devices. File a structured bug for an iOS keyboard issue; link it to the PR.
- Thursday. Run a 90-minute exploratory session against staging. Try the things the team did not predict. Write up findings.
- Friday. Sign off the QA checklist on a feature that has cleared review and verification. The signature is what closes the gate.

## Git etiquette

- **Small PRs.** One story per PR. If a story is too big, split the story first, not the PR.
- **PR descriptions link to the story.** `Implements [QUIZ-01](tasks/backend/QUIZ-01-session-service.md).`
- **Commits are cheap.** WIP commits are fine in-branch. Squash on merge if you like a clean history, or keep them if they tell a useful story.
- **Draft PRs are welcome.** Open a draft as soon as the branch has meaningful work. This gives teammates visibility and lets AI reviewers run early.
- **Rebase vs merge.** Team choice. Pick one and stick with it. Do not mix.

## Review etiquette

- **Read the linked story first.** A review without context is a waste of everyone's time.
- **Check against acceptance criteria.** Tick them off in the review.
- **One approval, at least one review.** Small teams can have "one approval = merge." Larger ones may want two.
- **Suggest, do not rewrite.** If you want it done differently, say so. Do not push commits to someone else's branch without asking.
- **Use AI to draft review comments.** But read them before submitting. The review is your accountability, not the AI's.

## The feedback loop

After every feature ships, spend 30 minutes in a retro:

- Did the artifacts help?
- Was the story breakdown the right size?
- Did reviewers catch the things they should have caught?
- Did AI outputs converge or diverge across team members?
- What do we change about our CLAUDE.md, our templates, or our habits?

Write the answers down. Ideally in `docs/retros/<date>.md`. The retro is itself an artifact.
