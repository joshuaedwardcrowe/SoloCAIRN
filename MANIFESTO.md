<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="logos/cairn-logo-dark-md.svg">
    <img alt="SoloCAIRN" src="logos/cairn-logo-light-md.svg" width="176">
  </picture>
</p>

# The SoloCAIRN Manifesto

We are building software with AI in our hands. This changes a lot, but not everything. The craft of shipping good product still depends on clear thinking, shared understanding, and honest feedback.

We have watched teams swing between two failure modes: ignoring AI entirely, or handing it the wheel. Both lose. We propose a third way.

## What we believe

### 1. Context is the product.

A well-written problem statement is worth ten prompts. A reviewed architecture doc saves a week of rework. The single highest-leverage thing you can do with AI is give it the same context a good engineer would have. That context lives in your repo, not in someone's head, not in a chat history, and not in Notion.

### 2. Artifacts over ceremony.

A short, honest markdown file beats a persona prompt every time. We value written artifacts that humans and AI can both read: problem statements, architectures, stories, checklists. We are suspicious of process that produces no artifacts.

### 3. Review is the stage gate.

The moment an idea, a design, or a piece of code meets another human for review is the moment quality actually happens. Pull requests are not just for code. Spec PRs and story PRs are how decisions get made. If the work is worth doing, it is worth reviewing. A gate is not a one-way door, though — see principle 11.

### 4. Humans lead, AI accelerates.

AI is an extremely capable assistant that has no stake in the outcome, no memory of last week, and no accountability to your users. Treat it accordingly. The person who owns the decision is a person. The person who owns the review is a person. AI drafts; humans decide.

### 5. Skip the costumes.

Assigning a persona to an AI ("you are a senior architect") looks load-bearing and usually is not. The wins multi-agent frameworks attribute to personas are mostly the context isolation and stage gates those frameworks happen to also provide. Get those directly: prompt with context, isolate with subagents, gate with reviews. Build your workflow around real artifacts, not maintained costumes.

### 6. Artifacts are operationally ephemeral, scoped to one feature.

Every SoloCAIRN artifact is in active use only for the duration of the feature build. They live in a dedicated SoloCAIRN repo or on a long-lived feature branch that never merges, are reviewed during the build, and stop being load-bearing the moment the feature ships. The code repo's `main` never sees them. Code is what survives as the operational truth.

Artifacts may remain in git history (in the SoloCAIRN repo, in the closed PR) as a historical record. That is acceptable: the goal is to keep them out of the *active workflow* and out of the code repo's main, not to delete every trace. SoloCAIRN does not own project-level documentation; that is your team's call.

### 7. Small is beautiful.

A 200-word problem statement beats a 10-page PRD. A one-page architecture doc beats a 40-slide deck. Every artifact has a minimum useful size and a maximum useful size. We aim for the former.

### 8. Roles stay human.

Business analysts, UX designers, team leads, developers, testers: these are real jobs done by real people with real judgment. SoloCAIRN gives each of them clearer artifacts and clearer handoffs. It does not replace them with a prompt.

### 9. Machines gate mechanics, humans gate decisions.

Human review is the gate for decisions: the design, the scope, the tradeoff. It is the wrong gate for rules that must hold every single time. The formatter passing, the required check being green, a change staying inside its agreed scope: these are non-negotiable and mechanical, and human memory does not enforce them at 100%. Put the binary, always-or-never rules in a machine that fails loudly. Keep the judgment with the humans.

### 10. The producer verifies first; review is the last guard.

Whoever makes the work checks it before a reviewer sees it. You do not hand over a first draft and outsource the checking. The reviewer's job is to catch what verification missed, not to do the verification. This holds for humans and for AI: AI should run the tests, check its output against the story, and surface what it could not resolve, rather than handing back something plausible for a human to debug.

### 11. Loops beat gates.

A stage gate that never gets revisited is a promise made before you had enough information to keep it. That is the one place upstream CAIRN leans Waterfall: Design fully decided before Breakdown, Breakdown fully decided before Build, and only one feedback loop drawn — Operate back to the *next* feature's Discovery. SoloCAIRN keeps CAIRN's stage-gated shape but insists every gate stays open to revision within the same feature: Design can be revised mid-Build, Scope can be revised mid-Breakdown, a story can be rewritten mid-implementation — as a small, fast PR against the artifact that was wrong, not a note for the next feature's retro. Approval means "enough to act on," never "correct forever."

### 12. Written for the next person, not just the last.

The measure of whether an artifact is good enough is not whether the person who wrote it understands it — it is whether a completely different human, with no conversation history and no memory of how the decision was made, could read the repo and pick up exactly where things left off. This applies equally to AI-authored planning: a WAG, a spike's findings, a scope decision worked out in conversation. If it only lives in a chat transcript or an AI's private context, it is not written down yet, no matter how thorough the conversation was.

## What we are not saying

- We are not saying AI is bad. We use it daily and it makes us faster.
- We are not saying process is bad. We are saying ceremony is bad.
- We are not saying every team should adopt SoloCAIRN. If what you have works, keep it.
- We are not promising a silver bullet. This is a set of habits for the build phase of a feature. The habits compound, but they do not replace runbooks, prioritisation, onboarding, or the thousand other things real teams need.
- We are not solving project-level documentation. That is a different problem; we leave it to your team.

## The shortest possible summary

> Keep your code repo's `main` for code. Keep feature scaffolding (problem, scope, architecture, stories) somewhere else, reviewed like code. Let AI read it. Let humans decide. End it when the feature ships.

That is SoloCAIRN.
