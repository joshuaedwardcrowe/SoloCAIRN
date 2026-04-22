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

### 5. No costumes.

Assigning a persona to an AI ("you are a senior architect") is theatre. It adds stylistic noise and rarely improves reasoning. What looks like persona value in multi-agent frameworks is almost always context isolation and stage gates doing the real work. We keep those and drop the costumes.

### 6. Artifacts are ephemeral, scoped to one feature.

Every CAIRN artifact is born with a feature and dies with it. They live in a dedicated CAIRN repo or on a long-lived feature branch that never merges, are reviewed during the build, and end when the feature ships. The code repo's `main` never sees them. Code is what survives. CAIRN does not own project-level documentation; that is your team's call.

### 7. Small is beautiful.

A 200-word problem statement beats a 10-page PRD. A one-page architecture doc beats a 40-slide deck. Every artifact has a minimum useful size and a maximum useful size. We aim for the former.

### 8. Roles stay human.

Business analysts, UX designers, team leads, developers, testers: these are real jobs done by real people with real judgment. CAIRN gives each of them clearer artifacts and clearer handoffs. It does not replace them with a prompt.

## What we are not saying

- We are not saying AI is bad. We use it daily and it makes us faster.
- We are not saying process is bad. We are saying ceremony is bad.
- We are not saying every team should adopt CAIRN. If what you have works, keep it.
- We are not promising a silver bullet. This is a set of habits. The habits compound.

## The shortest possible summary

> Write clear docs in a place that is not your code repo's main. Review them. Let AI read them. Let humans decide. End them when the feature ships.

That is CAIRN.
