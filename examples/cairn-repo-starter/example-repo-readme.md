# <Team or product name> ACAIRN

This repo holds the **ACAIRN artifacts** for our team's work: problem statements, scope, architecture, stories, QA checklists, and retros.

We follow [ACAIRN](https://link-to-the-cairn-methodology), an AI-assisted software development methodology by Abdullah Siddique. The short version: artifacts live here while a feature is being built, and end when the feature ships. The code lives in our code repo and is what survives.

## What is here

```
features/                ← active features, one folder each
archive/                 ← shipped features (kept for reference)
```

## How we work

For each new feature:

1. Create a folder under `features/<feature-slug>/`.
2. Open an ACAIRN PR with the problem statement. Reviewers: <list your team's typical reviewers>.
3. Layer in scope, architecture, stories, QA checklist via subsequent PRs.
4. Build the code in our code repo at <link to code repo>. Code PRs in that repo link to the relevant story file here using an **absolute URL** in the form `https://<git-host>/<org>/<this-repo>/blob/main/features/<feature>/stories/<platform>/<STORY-ID>.md`. Filesystem-relative paths render in your IDE but do not resolve in PR review UIs across repos.
5. When the feature ships and stabilises, write a `retro.md`, then move the folder to `archive/`.

## Setup for working with this repo

Clone this repo alongside the code repo:

```
git clone <code-repo-url> ~/work/<product>
git clone <this-repo-url> ~/work/<product>-cairn
```

Open both folders in your IDE workspace so AI sessions can read both.

## Conventions

- File names: kebab-case markdown (`problem-statement.md`, not `Problem Statement.md`).
- Story IDs: `<PROJECT>-<NN>` (for example, `QUIZ-01`).
- PRs: short, focused, one artifact or one logical batch at a time.
- No commits straight to `main`; everything via PR.

## Templates

Our adapted ACAIRN templates: <link to wherever you keep them, or a `templates/` folder in this repo>.

## Pointers

- The ACAIRN methodology: <link>
- Our team's coding conventions: <link in the code repo>
- Our team's contact channel: <Slack/Teams channel>
- Maintainer: <name>
