# 02. Philosophy

The [MANIFESTO](../MANIFESTO.md) gives you the one-page version. This is the director's cut: the same principles with the reasoning behind each, and the edge cases where they bend.

## 1. Context is the product

**The principle.** The primary artifact of modern software work is not code. It is the shared, reviewed understanding of what you are building and why. Code is a consequence of that understanding.

**Why it matters now.** Before AI, context mostly lived in people's heads because that was the cheapest place to put it. Writing everything down was prohibitively slow. AI collapses that cost. You can now draft a solid problem statement in twenty minutes that would have taken a full afternoon. The economics have changed, and the optimal amount of written context is much higher than it used to be.

**How to apply it.**
- Start any non-trivial feature with a written problem statement, even if it is short.
- If a decision was made verbally, write it down somewhere in the repo before end of day.
- When AI gives you a surprisingly good answer, ask yourself what context made that possible and preserve it.

**Where it bends.** For a one-line bug fix or a five-minute exploratory spike, writing context is overhead. Skip it. The point is proportionality, not ceremony.

## 2. Artifacts over ceremony

**The principle.** Every part of your process should produce a durable, readable artifact. Process that produces nothing but meetings is suspect.

**Why it matters.** Artifacts survive. Meetings do not. If an architecture decision exists only in a call that three people attended, it will be re-litigated next month, probably badly. If it exists in a two-page markdown file in the repo, it can be read, challenged, and updated.

**How to apply it.**
- Every recurring meeting should produce a written output. If it consistently does not, the meeting probably should not exist.
- Prefer async review of artifacts over synchronous alignment meetings.
- When you write an artifact, write it for someone joining the team in six months, not just for today's audience.

**Where it bends.** Brainstorming and interviews need a space to be messy before they become artifacts. Do not force polish too early. But do force a summary afterwards.

## 3. Review is the stage gate

**The principle.** Nothing graduates from one phase to the next without human review. Not specs, not architectures, not stories, not code. The review is the stage gate, and the pull request is the review.

**Why it matters.** Quality is produced at the point of disagreement. When a reviewer pushes back on a spec, the spec gets better. When a reviewer spots a hole in an architecture, the architecture gets better. If there is no review, there is no stage gate, and the work just slides from one phase to the next until it hits a bug in production.

**How to apply it.**
- Spec PRs: docs-only pull requests that are reviewed like code.
- Story PRs: story files reviewed before any implementation starts.
- Code PRs: linked to stories, reviewed against acceptance criteria.
- Approvals come from humans with skin in the game, not from bots.

**Where it bends.** For a solo developer, self-review after a night's sleep is a reasonable substitute. For truly time-critical production fixes, you ship first and review after, but then you *do* review, retrospectively.

## 4. Humans lead, AI accelerates

**The principle.** Decisions are made by humans. Judgment calls are made by humans. Accountability lives with humans. AI is an extraordinarily fast drafter, searcher, and expander. It is not a decider.

**Why it matters.** AI is trained to be agreeable. It will build whatever you ask, even if you are asking the wrong thing. The value of a human in the loop is that humans notice when the question itself is wrong. Removing the human does not make the process faster, it makes it faster-to-wrong.

**How to apply it.**
- Use AI to draft artifacts, then edit them until they are yours.
- Use AI to expand bullet points into prose, not to invent the bullet points.
- When AI proposes an architecture, treat it like a proposal from a capable but context-free new hire. Useful input, not a decision.

**Where it bends.** For highly bounded tasks with clear specifications (converting a format, generating boilerplate, writing a test for a known interface), AI can be trusted more directly. The pattern is: the more explicit the spec, the more latitude the AI gets.

## 5. No costumes

**The principle.** Do not prompt an AI to act as a persona. "You are a senior architect." "You are a product manager." This is theatre.

**Why it matters.** Research on role-prompting is clear: it adds stylistic noise and rarely improves reasoning. What looks like persona value in multi-agent frameworks is almost always the benefit of context isolation and stage gates, which you can get without the costume.

**How to apply it.**
- Prompt with context and goals, not identities.
- Get context isolation through separate conversations or subagents, not through personas.
- If you want AI to behave like a specialist, give it specialist-grade context (the artifacts) instead of a specialist costume.

**Where it bends.** Very short, well-defined role cues ("respond as a code reviewer focused on security") can be useful for single-turn tasks. The anti-pattern is building a whole workflow around maintained personas.

## 6. One repo, one source of truth

**The principle.** The code, the docs, the stories, and the conventions all live in the same repo. They are versioned together, reviewed together, and moved together.

**Why it matters.** Drift is silent and corrosive. When docs live in Notion and code lives in Git, the docs will lie within three months and nobody will know when the lie started. When they live together, a PR that changes the behavior also changes the doc, and the diff makes the change visible.

**How to apply it.**
- Problem statements, scope, architecture: in the repo.
- Stories: in the repo.
- Conventions, checklists, onboarding notes: in the repo.
- AI context files (CLAUDE.md, .cursor/rules, etc.): in the repo.

**Where it bends.** Organisation-level strategy docs, HR policies, and legal artifacts belong elsewhere. The rule is for product and engineering artifacts that describe the system being built.

## 7. Small is beautiful

**The principle.** Every artifact has a minimum useful size and a maximum useful size. Aim for the minimum.

**Why it matters.** A 200-word problem statement gets read. A 20-page PRD gets skimmed and then ignored. A two-page architecture gets discussed. A 50-page one gets a rubber-stamp. The value of a doc is proportional to the number of people who actually read it.

**How to apply it.**
- If an artifact is longer than it needs to be, cut it.
- Use bullets and tables aggressively. Paragraphs are for when you need to explain *why*.
- When in doubt, link rather than repeat.

**Where it bends.** Compliance and regulatory contexts sometimes require length for its own sake. Accept it, but keep a short executive summary at the top.

## 8. Roles stay human

**The principle.** CAIRN is a methodology for teams of humans who use AI. It does not pretend that a prompt is a business analyst. It does not pretend that a subagent is a UX researcher.

**Why it matters.** The work of a good BA is not producing a document. It is sitting in a room with a stakeholder, noticing what they did not say, and asking the follow-up question. The work of a good UX researcher is not drawing wireframes. It is watching a user fail a task and understanding why. These are human activities. AI can speed up the writing-up afterwards, but it cannot do the interviews, the noticing, or the judging.

**How to apply it.**
- Each role in [roles/](../roles/) defines what a human does, and how AI supports that.
- If AI is doing the noticing or the deciding for a role, you have made a mistake.

**Where it bends.** For very small teams, one person may wear multiple hats. That is fine. The hats are still human.

## The principles in one sentence each

1. Context is the product.
2. Process should leave artifacts.
3. Review is the real gate.
4. Humans decide, AI drafts.
5. Costumes do not help.
6. Everything lives in the repo.
7. Smaller is usually better.
8. Roles are human.

If you remember nothing else, remember these eight sentences.
