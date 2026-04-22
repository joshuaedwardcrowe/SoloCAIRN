# The CAIRN Manifesto

We are building software with AI in our hands. This changes a lot, but not everything. The craft of shipping good product still depends on clear thinking, shared understanding, and honest feedback.

We have watched teams swing between two failure modes: ignoring AI entirely, or handing it the wheel. Both lose. We propose a third way.

## What we believe

### 1. Context is the product.

A well-written problem statement is worth ten prompts. A reviewed architecture doc saves a week of rework. The single highest-leverage thing you can do with AI is give it the same context a good engineer would have. That context lives in your repo, not in someone's head, not in a chat history, and not in Notion.

### 2. Artifacts over ceremony.

A short, honest markdown file beats a persona prompt every time. We value durable artifacts that humans and AI can both read: problem statements, architectures, stories, checklists. We are suspicious of process that produces no artifacts.

### 3. Review is the stage gate.

The moment an idea, a design, or a piece of code meets another human for review is the moment quality actually happens. Pull requests are not just for code. Spec PRs and story PRs are how decisions get made. If the work is worth doing, it is worth reviewing.

### 4. Humans lead, AI accelerates.

AI is an extremely capable assistant that has no stake in the outcome, no memory of last week, and no accountability to your users. Treat it accordingly. The person who owns the decision is a person. The person who owns the review is a person. AI drafts; humans decide.

### 5. Be skeptical of costumes.

Assigning a persona to an AI ("you are a senior architect") looks load-bearing and usually is not. The wins multi-agent frameworks attribute to personas can mostly be explained by the context isolation and stage gates those frameworks happen to also provide. The evidence is mixed and the field moves; we are not claiming proof. We are claiming the simpler thing first: prompt with context, isolate with subagents, gate with reviews. If a costume helps after that, fine. If you find yourself maintaining personas as core process, you have probably bought complexity for unclear return.

### 6. Artifacts are operationally ephemeral, scoped to one feature.

Every CAIRN artifact is in active use only for the duration of the feature build. They live in a dedicated CAIRN repo or on a long-lived feature branch that never merges, are reviewed during the build, and stop being load-bearing the moment the feature ships. The code repo's `main` never sees them. Code is what survives as the operational truth.

Artifacts may remain in git history (in the CAIRN repo, in the closed PR) as a searchable record. That is acceptable: the goal is to keep them out of the *active workflow* and out of the code repo's main, not to delete every trace. CAIRN does not own project-level documentation; that is your team's call.

### 7. Small is beautiful.

A 200-word problem statement beats a 10-page PRD. A one-page architecture doc beats a 40-slide deck. Every artifact has a minimum useful size and a maximum useful size. We aim for the former.

### 8. Roles stay human.

Business analysts, UX designers, team leads, developers, testers: these are real jobs done by real people with real judgment. CAIRN gives each of them clearer artifacts and clearer handoffs. It does not replace them with a prompt.

## What we are not saying

- We are not saying AI is bad. We use it daily and it makes us faster.
- We are not saying process is bad. We are saying ceremony is bad.
- We are not saying every team should adopt CAIRN. If what you have works, keep it.
- We are not promising a silver bullet. This is a set of habits for the build phase of a feature. The habits compound, but they do not replace runbooks, prioritisation, onboarding, or the thousand other things real teams need.
- We are not solving project-level documentation. That is a different problem; we leave it to your team.

## The shortest possible summary

> Keep your code repo's `main` for code. Keep feature scaffolding (problem, scope, architecture, stories) somewhere else, reviewed like code. Let AI read it. Let humans decide. End it when the feature ships.

That is CAIRN.
