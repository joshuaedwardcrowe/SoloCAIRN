# 08. Adopting CAIRN on a team

You cannot mandate CAIRN into a team and expect it to stick. But you can roll it in gradually, starting with one feature, proving the value, and letting the habits spread.

Here is how.

## Phase 0: Decide whether it fits

Before adopting anything, answer honestly:

- **Is AI already part of your team's daily work?** If not, CAIRN is overkill. Pick the individual pieces that help.
- **Do you have a multi-role team?** (BA, UX, devs across platforms.) If it is all one role, the lifecycle doc is less relevant. Still, the three-PR model helps.
- **Do you control the repo?** If you cannot put docs in the code repo, the "in-repo" premise collapses. Fix that first.
- **Is there a real person willing to own the rollout?** Someone has to care. It does not have to be the most senior person, but it has to be a credible one.

If you answered yes to most of those, continue.

## Phase 1: Pilot on one feature

Do not announce "we're adopting CAIRN." That guarantees resistance.

Instead, pick the next non-trivial feature. Propose to the team: *"For this feature, let's try writing the problem, scope, and architecture as markdown in the repo first, then breaking it into stories, then building. I'll lead the writing. We'll retro afterwards."*

**What to produce on the pilot.**
- Spec PR (problem, scope, architecture). Short. Half a page each is fine.
- Story PR (stories in `tasks/<platform>/`).
- Code PRs linked to stories.

**What to skip on the pilot.**
- Elaborate templates.
- UX research docs if UX is not involved in this feature.
- Runbooks, unless the feature needs one.

Keep it lean. The goal is to feel the shape, not to produce every possible artifact.

**After the pilot.** Hold a 30-minute retro. Three questions:
1. Did the docs help?
2. Did review catch things?
3. What would we cut, keep, or change?

Write the answers down. That is your first method-retro artifact.

## Phase 2: Formalise the templates

Once the pilot has shown value, copy the CAIRN templates into the repo and adapt them:

- Strip sections you did not use on the pilot.
- Add sections you needed but the template lacked.
- Rename things to match your team's language.

The templates should feel like yours within a week.

**Also in Phase 2.** Write your team's `CLAUDE.md` (or equivalent). Include:
- The project's stack and layout.
- Where to find `docs/` and `tasks/`.
- Your conventions.
- The never-do list.

This is the highest-leverage file in the repo. Spend time on it.

## Phase 3: Scale to the whole team

Now apply CAIRN to every non-trivial feature. Small stuff still moves through the direct code-PR path; anything with meaningful design, cross-platform impact, or stakeholder involvement goes through Spec PR first.

**Signals you are on track.**
- New team members can find the active feature's spec within five minutes.
- AI sessions from different devs produce consistent-feeling output.
- Reviewers push back on specs as often as they push back on code.
- You occasionally kill a feature at the Spec PR stage because writing it down revealed it was not worth building. (This is one of the biggest wins.)

**Signals you are drifting.**
- Specs getting written after the code.
- Stories that take two weeks.
- PRs approved in seconds with no comments.
- Team members bypassing the process for "urgent" work that turns out not to be urgent.

When you see drift, go back to the anti-patterns doc and name what is happening.

## Phase 4: Retrospect and adjust

Every quarter, spend an hour asking:

- Which templates earn their keep? Which do not?
- Which stages are we skipping? Why?
- Where is AI helping most? Where is it hurting?
- What has our team added to CAIRN that works? Document it.
- What have we dropped that should come back?

Update the templates and docs in the same PR where you decide the changes. The method itself lives in the repo and moves through PRs, like everything else.

## Handling common objections

### "We already have a process."

Good. CAIRN is compatible with most lightweight agile variants. You probably already produce some of these artifacts. The question is whether they live in the repo and are reviewed like code. If yes, you are most of the way there. If no, that is the change to make.

### "This is just agile with extra steps."

It is agile minus some steps (no story-point ceremony, no stand-up reporting, no sprint rituals if you do not want them) plus an emphasis on durable artifacts and AI context. Take what helps, ignore the rest.

### "We don't have time to write docs."

You have time to re-litigate decisions, to rebuild context after every handoff, and to fix bugs that came from misunderstanding. That time can go into the artifact instead. The artifact is the cheaper option when the cost of writing is one AI-assisted draft away.

### "The AI will do all this for us anyway."

AI will do it *badly* without human context and human review. That is the exact failure mode CAIRN is built to prevent. If AI was a perfect decider, the whole methodology would be unnecessary. AI is not a perfect decider. Hence the method.

### "We tried BMAD/another framework, it didn't stick."

Ask why. Usually the answer is "too heavy" or "the personas were confusing." CAIRN is designed to be what is left when you strip those things away. It may fit where heavier frameworks did not.

### "Our organisation uses Jira/Confluence/etc."

Fine. Keep Jira for tickets and Confluence for organisational content. But keep your specs, stories, architecture, and conventions in the code repo. The two can coexist; the repo is canonical for things about the code, and the other tools are views or pointers.

## The smallest viable adoption

If you only do three things:

1. **Start your next feature with a Spec PR.** Problem, scope, and a paragraph on approach. Merge it before any code.
2. **Write a `CLAUDE.md`.** One page. Conventions and pointers.
3. **Put stories in the repo.** One file per story, one story per PR.

That is a 90%-value adoption with 10% of the effort. Everything else is refinement.

## Where it goes next

Once CAIRN habits are real, you can start adding the optional pieces: runbooks, postmortems, per-feature retro docs, shared subagent prompts. But do not lead with those. Lead with specs, stories, and AI context. The rest compounds.
