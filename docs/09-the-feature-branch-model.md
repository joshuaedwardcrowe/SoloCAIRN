# 09. The feature branch model

CAIRN artifacts are scaffolding. They exist to coordinate humans and AI through the work of building one feature. Once the feature ships and stabilises, the code is the documentation. The artifacts have done their job.

This doc describes how to make that lifecycle real in git.

## The principle

> Every CAIRN artifact is born with a feature and dies with the feature.

The artifacts never reach `main`. They live on a dedicated feature branch, are reviewed there, evolve there, and are closed without merging when the feature is released and stable.

The code, of course, does merge. CAIRN is silent on how your code branches and PRs work. The model below applies only to the CAIRN scaffolding.

## What CAIRN is and is not for

**CAIRN is for.** Building one feature with humans and AI. Problem framing, scoping, design coordination, story breakdown, QA gating. All of this is short-lived: weeks to a few months.

**CAIRN is not for.** Project-level documentation: system architecture as it currently stands, schema as currently deployed, runbooks, conventions, the project's AI context file. Whether and how a team maintains those is a separate question. CAIRN does not take a position. They live wherever your team decides, on `main` or elsewhere.

If your team has no project-level documentation today, CAIRN does not require you to start. The scaffolding is feature-scoped and complete in itself.

## The git layout

For each new feature:

```
main                          ← never sees CAIRN artifacts
  └── cairn/<feature-slug>    ← long-lived branch holding all artifacts
        └── PR to main        ← long-lived PR, NEVER merged, closed at release
```

For the code:

```
main
  ├── feat/<story-id>-...     ← code branches as your team normally works
  ├── feat/<story-id>-...     ← merge to main per your normal process
  └── feat/<story-id>-...
```

The `cairn/<feature-slug>` branch and the code branches are independent. They reference each other by URL, not by shared file paths.

## What lives on the feature branch

Everything CAIRN produces for this feature:

```
cairn/pub-quiz-live-scoring (branch)
  docs/features/pub-quiz/
    problem-statement.md
    stakeholder-interviews.md
    ux-research.md
    scope.md
    architecture.md           ← feature-level architecture only
    open-questions.md
    qa-checklist.md
  tasks/pub-quiz/
    backend/
    frontend/
    mobile/
    database/
```

This branch never merges into `main`. The PR opened against `main` is the long-lived review surface for the artifacts.

## The lifecycle

1. **Branch creation.** When a feature is greenlit, create `cairn/<feature-slug>` from current `main`.
2. **Spec PR.** Open a PR from this branch to `main`. Title it clearly: "[CAIRN] Pub Quiz Live Scoring (do not merge)." This is the long-lived PR.
3. **Iterate.** Problem, research, scope, architecture, stories all land on this branch through reviewed sub-PRs (small, targeted, against the feature branch) or directly with team conventions for review-on-branch.
4. **Build.** Code happens on `feat/*` branches off `main`, merging to `main` per your team's normal flow. Each code PR description links to its story file by URL on the feature branch.
5. **QA.** The QA checklist lives on the feature branch and is updated as work proceeds.
6. **Release.** Code is in `main` and behind a flag (or however you ship). The feature is rolled out and stabilises.
7. **Close.** Once stable (your call: a week, a month, after the pilot), close the long-lived PR with a comment summarising the outcome. Delete the `cairn/<feature-slug>` branch if your team prefers; the closed PR remains forever and is addressable by URL.

The closed PR is the historical record. The diff, the conversation, the file tree, all permanent and linkable.

## How AI sessions reach the artifacts

Code PRs branch from `main` and do not include the CAIRN artifacts in their working tree. AI sessions running against a code branch need access to the feature branch's docs. Two simple options:

**Option A: git worktree.**
```
git worktree add ../my-repo-cairn cairn/<feature-slug>
```
Now the dev has a sibling directory with all the CAIRN artifacts checked out. AI sessions can be pointed at it.

**Option B: fetch and read.**
The dev fetches the feature branch and reads files from it directly:
```
git fetch origin cairn/<feature-slug>
git show origin/cairn/<feature-slug>:docs/features/pub-quiz/architecture.md
```
Or using a sparse checkout into a sibling folder.

Pick whichever fits your tooling. The point is that the artifacts are reachable from any developer's machine without ever touching `main`.

## What survives in main

Nothing CAIRN-shaped. The only things that should land in `main` as a consequence of building a feature are:

- The code itself.
- Any project-level changes the team would have made anyway: schema migrations, runbook updates, system architecture deltas, and so on. These are not CAIRN artifacts; they are operational truth, and how your team handles them is outside CAIRN's scope.

If your team has no project-level docs convention today, none of those updates are required. The code merges; that is the only trace.

## Discoverability across teams

At small scale (one team, a few features per quarter), no extra discoverability is needed. Open PRs are visible.

At larger scale (multiple teams sharing a repo or domain), if you want lightweight visibility into who is working on what, this is a project-level concern, not a CAIRN one. Some options teams have used:

- A pinned issue listing active CAIRN feature branches.
- A simple convention: every CAIRN PR title is prefixed `[CAIRN]` so the PR list filters cleanly.
- A dashboard that lists open PRs matching that convention.

CAIRN does not prescribe any of these. Pick what suits your organisation.

## Why this works

- **Main stays clean forever.** No team's CAIRN history accumulates on `main`. Search results, file trees, and tooling are unaffected.
- **No doc rot.** Artifacts cannot drift from code if they never live with the code post-release. They were true when the feature shipped; that is all they ever needed to be.
- **Forensics still possible.** Closed PRs are permanent. "What was the spec for feature X?" has a URL answer.
- **Scales to many teams.** Each team's CAIRN work is invisible to others by default. Cross-team coordination happens through whatever org-level mechanisms already exist, not by polluting the codebase.

## Why this might not suit you

- **Compliance regimes** that require persistent, in-repo documentation will not accept "the closed PR is the record." If you operate in such a regime, merge the artifacts into `main` under a clearly-archived path and accept the bloat.
- **Teams without git platforms that preserve closed PRs** lose the historical record. Most modern platforms (GitHub, GitLab, Bitbucket, Azure DevOps) preserve them indefinitely; verify yours.
- **Teams that genuinely value re-reading specs years later** as a primary onboarding path. Most teams overestimate this; if yours actually does it, keep them on `main`.

## A summary you can paste into your team docs

> CAIRN artifacts live on a dedicated `cairn/<feature>` branch with a long-lived PR to main that never merges. Code merges to main as normal. When the feature ships and stabilises, the CAIRN PR is closed. The closed PR remains as the historical record. Project-level documentation (system architecture, schema, runbooks, conventions) is out of CAIRN's scope and is handled by your team's existing conventions.
