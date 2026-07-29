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

**The principle.** Every part of your process should produce a written, readable artifact. Process that produces nothing but meetings is suspect.

**Why it matters.** Written artifacts can be read, challenged, and updated. Meetings cannot. If an architecture decision exists only in a call that three people attended, it will be re-litigated next month, probably badly. If it exists in a two-page markdown file in the ACAIRN repo, the team and the AI can both work from it.

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

## 5. Be skeptical of costumes

**The principle.** Be skeptical of prompting an AI to maintain a persona ("You are a senior architect", "You are a product manager") as a load-bearing part of your workflow. The evidence we have suggests these role prompts mostly add stylistic noise without consistently improving reasoning, and the wins that multi-agent frameworks claim from "personas" can usually be explained more simply by the context isolation and stage gates those frameworks happen to also provide.

We are not claiming this is a settled empirical result; published findings on role-prompting are mixed and the field moves quickly. We are claiming that personas are at best a modest effect, often zero, and that building a methodology around them buys complexity for unclear return.

**Why it matters.** If you build your process on persona agents, you commit to maintaining their prompts, debugging their interactions, and explaining them to new joiners. If the underlying value is context isolation and stage gates, you can get those for free with subagents and PR review, with none of the costume overhead.

**How to apply it.**
- Prompt with context and goals, not identities.
- Get context isolation through separate conversations or subagents, not through personas.
- If you want AI to behave like a specialist, give it specialist-grade context (the artifacts) instead of a specialist costume.

**Where it bends.** Very short, single-turn role cues ("respond as a code reviewer focused on security") seem to land more reliably than maintained multi-turn personas. Use them when they help. The anti-pattern we want to avoid is building a whole workflow around maintained, named personas with their own configuration.

**Field evidence.** We tested a maintained multi-agent team (a "developer", a "designer", a "content strategist") on a real build. The value that actually showed up was the separate contexts and a concrete review rubric held by one agent: the reviewer withheld sign-off on specific defects and caught real bugs. The "you are a senior designer" framing did almost none of the work; the checklist and the isolated context did it. Stripping the persona language and keeping what was load-bearing (scope, criteria, tool access) left a tool that was easier to reason about and just as useful. One data point, consistent with the principle: the costume was the disposable part.

## 6. Artifacts are operationally ephemeral and feature-scoped

**The principle.** A ACAIRN artifact is in active use only for the duration of one feature build. It is the scaffolding the team and AI work from while building. Once the feature ships and stabilises, the artifact stops being load-bearing: the code is the operational truth from that point on.

This is *operational* ephemerality, not deletion. The artifact may remain in the ACAIRN repo's history or in a closed PR as a historical record. The goal is to keep it out of the active workflow and out of the code repo's `main`, not to wipe every trace.

**Why it matters.** If artifacts merged into the code repo's `main`, every team's history would accumulate there and `main` would drown in old specs, dead stories, and rotting docs that contradict the current code. By keeping artifacts off `main`, the code repo stays clean indefinitely. The historical record (if you want one) lives somewhere it cannot pollute the working tree.

**How to apply it.** Pick one of two deployment models. They are not equally strong:

- **A separate ACAIRN repo (recommended)**: a dedicated repo holds your team's or company's ACAIRN artifacts. Devs clone it alongside the code repo. The code repo is untouched. Old features are archived to a folder or deleted from the working tree (git history preserves them either way). Structurally sound, no git anti-patterns, recommended for most teams.
- **A long-lived branch in the code repo (fallback only)**: a `cairn/<feature>` branch holds the artifacts; a PR is opened against `main` and never merged. Closed at release. Use this only when you genuinely cannot create a separate repo. Comes with real ergonomic and audit-tool costs documented in [09-deployment-models.md](09-deployment-models.md).

In both cases: code merges to `main` through your team's normal flow, with code PRs linking to artifacts in the chosen location.

**What ACAIRN does not own.** Project-level documentation: system-level architecture, current schema, runbooks, conventions, the project's AI context file. Whether and how a team maintains those is outside ACAIRN's scope, decided by the team or the company. ACAIRN is for one feature at a time and ends with that feature. We are honest about this rather than pretending the problem does not exist; see [10-what-cairn-does-not-solve.md](10-what-cairn-does-not-solve.md) for what to do about the things we leave on the table.

**Where it bends.** Compliance regimes that require persistent in-repo documentation will not accept the ephemeral model. If you operate in such a regime, merge the artifacts into the code repo's `main` under a clearly-archived path and accept the bloat.

## 7. Small is beautiful

**The principle.** Every artifact has a minimum useful size and a maximum useful size. Aim for the minimum.

**Why it matters.** A 200-word problem statement gets read. A 20-page PRD gets skimmed and then ignored. A two-page architecture gets discussed. A 50-page one gets a rubber-stamp. The value of a doc is proportional to the number of people who actually read it.

**How to apply it.**
- If an artifact is longer than it needs to be, cut it.
- Use bullets and tables aggressively. Paragraphs are for when you need to explain *why*.
- When in doubt, link rather than repeat.

**Where it bends.** Compliance and regulatory contexts sometimes require length for its own sake. Accept it, but keep a short executive summary at the top.

## 8. Roles stay human

**The principle.** ACAIRN is a methodology for teams of humans who use AI. It does not pretend that a prompt is a business analyst. It does not pretend that a subagent is a UX researcher.

**Why it matters.** The work of a good BA is not producing a document. It is sitting in a room with a stakeholder, noticing what they did not say, and asking the follow-up question. The work of a good UX researcher is not drawing wireframes. It is watching a user fail a task and understanding why. These are human activities. AI can speed up the writing-up afterwards, but it cannot do the interviews, the noticing, or the judging.

**How to apply it.**
- Each role in [roles/](../roles/) defines what a human does, and how AI supports that.
- If AI is doing the noticing or the deciding for a role, you have made a mistake.

**Where it bends.** For very small teams, one person may wear multiple hats. That is fine. The hats are still human.

## 9. Gate mechanics with machines, decisions with humans

**The principle.** Rules that must hold every single time should not depend on anyone remembering them. Human review is the gate for decisions. It is the wrong gate for mechanics.

**Why it matters.** Principle 3 puts the stage gate on human judgment, and for decisions that is exactly right: is this the correct design, is the scope honest, is the tradeoff acceptable. But a second class of rule is non-negotiable and mechanical: the formatter must pass, the required check must be green, this change must stay inside the agreed scope. Those do not need judgment, they need to be true 100% of the time, and human judgment does not scale to 100%. The one time a tired reviewer waves through an unformatted diff or an out-of-scope edit, the rule failed silently. Intentions are not enforcement.

**How to apply it.**
- Split your gates in two. Humans gate decisions; deterministic checks gate mechanics.
- Make the mechanical non-negotiables binary and automatic: required status checks, branch protection, merge-blocking linters, scope checks. If a rule is "always" or "never," it belongs in a machine, not in a reviewer's memory.
- When a mechanical gate fails, it should fail loudly and block, not warn and continue. A gate that can be skipped without noticing is not a gate.

**Where it bends.** Do not mechanize judgment. A check that tries to enforce "is this good architecture" or "is this the right abstraction" becomes ceremony and noise, and people learn to route around it. Only make deterministic what is genuinely binary. Everything else stays with the humans, under principle 3.

## 10. The producer verifies first; review is the last guard

**The principle.** Whoever produces the work is responsible for checking it before it reaches a reviewer. You do not hand over a first draft and outsource the verification. This applies to humans and to AI equally.

**Why it matters.** Review is expensive and the reviewer starts cold: they have to reconstruct the context the producer already holds. If the producer hands over unverified work, the reviewer ends up doing the verification the producer should have done, at a much higher cost, and the actual purpose of review (catching what verification *missed*) never happens. The producer runs the acceptance criteria, exercises the change, and does an honest adversarial pass on their own output first. The reviewer is the last guard, not the first. This is doubly true when AI produced the work: AI should verify its own output aggressively (run the tests, check against the story, hunt its own diff for mistakes) and surface what it could not resolve, rather than handing back a plausible draft for a human to debug.

**How to apply it.**
- Before requesting review, the producer checks the work against the story's acceptance criteria and states plainly what was verified and what was not.
- Distinguish "it compiles" from "I ran it and it does what the story asks." Only the second counts as verified.
- When AI is the producer, the same bar applies: verified output with uncertainties surfaced, not a first draft with the checking left for the human.

**Where it bends.** Genuinely exploratory or spike work is handed over rough on purpose, to get direction before investing in polish. That is fine, but say so explicitly. The anti-pattern is handing over work that is *presented* as done while quietly relying on the reviewer to find the holes.

## The principles in one sentence each

1. Context is the product.
2. Process should leave artifacts.
3. Review is the real gate.
4. Humans decide, AI drafts.
5. Be skeptical of costumes.
6. Artifacts are operationally ephemeral, scoped to one feature.
7. Smaller is usually better.
8. Roles are human.
9. Machines gate mechanics, humans gate decisions.
10. The producer verifies first; review is the last guard.

If you remember nothing else, remember these ten sentences.
