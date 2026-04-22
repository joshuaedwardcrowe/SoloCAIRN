# 07. Anti-patterns

Things that look like CAIRN but are not. If you see these happening on your team, you have drifted. This doc exists to make the drift easy to name.

## Ceremony bloat

**What it looks like.** Stories with twelve mandatory sections. Problem statements that require three sign-offs. A weekly "CAIRN ritual" meeting that produces no artifact.

**Why it happens.** Well-meaning people add structure to prevent past failures. Every addition makes sense in isolation. The cumulative weight is what kills you.

**How to fix it.** Every quarter, run a ceremony audit. For each template, each mandatory field, each recurring meeting: what happens if we remove it? If nothing breaks in the next month, it was ceremony.

## Persona drift

**What it looks like.** Someone introduces `/architect`, `/analyst`, `/qa` as prompts. These become "agents." Now the team has ten AI personas with invented names and the team lead maintains their prompts in a wiki.

**Why it happens.** It feels legitimising. It looks like the multi-agent frameworks on Twitter. It gives people who love process something to configure.

**How to fix it.** Go back to unnamed prompts that reference real repo artifacts. If someone insists on personas, ask them to measure the quality delta against prompts that just reference the artifacts. The delta will not be there.

## Doc rot

**What it looks like.** The architecture doc describes a service that was renamed six months ago. The CLAUDE.md references a test runner you no longer use. The "conventions" doc contradicts the actual code.

**Why it happens.** Docs get written once, under pressure, and then nothing in the process requires them to stay current.

**How to fix it.**
- Make doc updates part of the definition of done. If the code change affects what's described in a doc, the doc changes in the same PR.
- In retros, name three docs at random and check them. If two are wrong, that is a process problem, not a motivation problem.
- Kill docs that have no natural update rhythm. A doc nobody updates is worse than no doc.

## Skipping the Spec PR

**What it looks like.** "This is urgent, let's just start building. We can write the docs after."

**Why it happens.** Pressure, excitement, or a belief that docs slow you down.

**Why it is dangerous.** The docs-after approach produces docs that describe what was built, not what was intended. The result is that next time you plan a similar feature, you are re-inventing the spec from code archaeology.

**How to fix it.** Write the Spec PR anyway, even if it takes two hours. If the feature is genuinely too urgent for two hours of writing, it is also too urgent for a proper implementation; ship a hack with a ticket to do it right.

## AI as decision-maker

**What it looks like.** "The AI chose this approach, so we went with it." "Copilot suggested the architecture, so we adopted it." "We asked Claude what to prioritise."

**Why it is dangerous.** AI does not weigh tradeoffs that require context outside the repo. It does not know your budget, your politics, your customers, or your risk tolerance. It will confidently recommend things that are plausible but wrong for your situation.

**How to fix it.** Enforce a rule: every decision-level output from AI (architectures, priorities, tradeoff calls) is reviewed and owned by a named human before it takes effect. "Claude proposed X, the team reviewed it, I decided X with modification Y" is fine. "We did X because the AI said so" is not.

## One giant story

**What it looks like.** A story titled "Implement the bulk signing feature," three pages long, with twenty-five acceptance criteria, that takes two weeks.

**Why it happens.** Breakdown is work, and it is tempting to skip it.

**Why it is dangerous.** Giant stories hide coordination problems. Two devs will unknowingly work on overlapping parts. The PR becomes un-reviewable. The "done" check becomes a matter of opinion instead of a checklist.

**How to fix it.** Enforce a size limit: if a story cannot fit in half a page and be done in three days, it is not a story, it is a feature. Break it down further.

## CAIRN artifacts outside git

**What it looks like.** The team agrees to adopt CAIRN, then puts the problem statement in Confluence, the stories in Jira, the architecture in Miro. The `cairn/<feature>` branch is empty.

**Why it happens.** Organisational inertia, tool-per-role mindset, or the belief that "docs belong in our wiki, not in code."

**Why it is dangerous.** AI sessions cannot easily reach those artifacts. Reviewers cannot use code-review tooling on them. Versioning is inconsistent. The whole point of CAIRN's branch model collapses if the artifacts are not in git.

**How to fix it.** CAIRN artifacts live on the `cairn/<feature>` branch as markdown, full stop. They never merge to `main`, so the "but our repo is for code" objection does not apply. Other tools (Jira, Confluence) keep doing their other jobs (tickets, organisational content). They are not where CAIRN artifacts live during the build.

## Merging the feature branch

**What it looks like.** Someone clicks merge on the long-lived Spec PR. Now `main` has all the CAIRN artifacts in it.

**Why it happens.** Habit. Long-lived PRs feel like they should eventually merge. Or someone is trying to "tidy up" by closing the open PR.

**Why it is dangerous.** Once artifacts are on `main`, you have started accumulating them per feature, per team. The clean-main property collapses. You now also have the doc-rot problem you were trying to avoid.

**How to fix it.** Title the PR clearly: `[CAIRN] Pub Quiz Live Scoring (do not merge)`. Set branch protection on `main` if you can. When the feature ships, **close** the PR. Never merge.

## Artifact theatre

**What it looks like.** Thick docs that nobody reads. Templates filled in with copy-paste placeholders and then forgotten. A 40-slide architecture deck.

**Why it happens.** Teams confuse "producing artifacts" with "the work." Writing a long doc feels productive even when nobody will read it.

**How to fix it.** For every artifact, name the reader and the decision it supports. If you cannot name them, cut it. Prefer a half-page that is actually read over five pages that are skimmed.

## Review theatre

**What it looks like.** PRs approved in 30 seconds with a rubber stamp. "LGTM" with no comments on complex changes. Reviews that never push back.

**Why it happens.** Cultural. Speed-optimised incentives. Reviewers who are too busy.

**Why it is dangerous.** If review is the stage gate and the gate is always open, there is no gate. Quality collapses quietly.

**How to fix it.** Measure it in retros: how many review comments, how many requested changes, how many catches. If the numbers are all zero, the process is broken. Celebrate reviewers who catch things. Make it explicit that approving a bad PR is worse than rejecting a good one.

## "The AI can handle it"

**What it looks like.** Teams skipping the hard thinking because "the AI will figure it out." Vague stories handed to AI with a shrug. Results reviewed only superficially.

**Why it happens.** The AI is very good at producing output that looks right. It is easy to believe, session by session, that you do not need the upstream discipline.

**Why it is dangerous.** The output is plausible, not correct. Over weeks, plausible-but-wrong accumulates. By the time it shows up as bugs, the context to fix it is long gone.

**How to fix it.** Keep the discipline. Spec PRs, story PRs, real human review. The AI makes those steps faster, not optional.

## The meta-anti-pattern

If you find yourself doing the method because the method says so, rather than because the artifact is about to support a real decision, you have lost the plot.

Every CAIRN artifact should feel like it is earning its keep right now. The moment it stops, change the artifact or cut it.
