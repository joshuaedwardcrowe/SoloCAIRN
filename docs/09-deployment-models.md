# 09. Deployment models: where the artifacts live

CAIRN artifacts are ephemeral. They are born with a feature, reviewed during the build, and end when the feature ships. The principle is fixed.

Where they physically live during their short life is a choice. There are two good options. Both honour the principle. Each has tradeoffs.

## The principle (unchanged either way)

> CAIRN artifacts never land on the code repo's `main`. They are scaffolding for the build, not documentation for posterity. The code is what survives.

What changes between the two models is the git topology: same repo on a non-merging branch, or a separate repo entirely.

## Option A: separate CAIRN repo (recommended for most teams)

A dedicated repo, owned by your team (or your company), holds all CAIRN artifacts. The code repo is left untouched. Devs clone both side by side and open them in the same IDE workspace so AI can cross-reference.

```
~/work/
├── my-product/         ← code repo (untouched by CAIRN)
└── my-team-cairn/      ← CAIRN repo
    └── features/
        ├── pub-quiz-live-scoring/
        │   ├── problem-statement.md
        │   ├── scope.md
        │   ├── architecture.md
        │   ├── stories/
        │   └── qa-checklist.md
        └── another-feature/
```

### How the work flows

1. **Branch creation.** When a feature is greenlit, create a folder under `features/<feature-slug>/` in the CAIRN repo and a branch `feat/<feature-slug>` in the CAIRN repo to land the initial artifacts.
2. **Spec PR.** Open a normal PR in the CAIRN repo against its `main`. Yes, this PR does merge: into the CAIRN repo's `main`, not the code repo's. The CAIRN repo's `main` is the working surface for in-flight features.
3. **Iterate.** Problem, research, scope, architecture, stories all land on the feature folder via reviewed PRs in the CAIRN repo.
4. **Build.** Code happens on `feat/*` branches off the code repo's `main`, merging to `main` per your team's normal flow. Each code PR description links to the artifact files by path within the CAIRN repo.
5. **Release.** The feature ships and stabilises.
6. **End of life.** When the feature is stable, move its folder from `features/<feature-slug>/` to `archive/<feature-slug>/`, or delete it. Your call. The CAIRN repo's git history is the historical record.

### When this fits

- You can spin up a new repo with reasonable speed.
- Your team wants the strongest possible decoupling between artifacts and code.
- Your tooling, AI or otherwise, sometimes struggles with authenticated cross-repo URLs.
- You want stakeholders, PMs, or BAs to access CAIRN artifacts without code repo permissions.

### Tradeoffs you accept

- New devs clone two repos instead of one. Modern IDE workspaces handle this trivially, but it is a setup step.
- Code reviewers on the code PR cannot browse the architecture doc in the same web UI. Mitigated by quoting key sections in the code PR description, or by reviewers having the CAIRN repo open in another tab.
- You cannot make atomic commits that touch both code and artifacts. This is rare and arguably correct: artifact updates and code changes deserve separate review.

### Granularity choice

Three reasonable shapes for the CAIRN repo itself:

| Shape | Best for | Watch out for |
|---|---|---|
| One CAIRN repo per team | Stable teams owning a clear product area | Cross-team discoverability is harder |
| One CAIRN repo per code repo | One code repo serving multiple teams | Harder if a team works across repos |
| One CAIRN repo per company | Cross-team learning, mobile teams | Accumulates fast, needs grooming |

Default to **per team** unless you have a specific reason to choose otherwise.

## Option B: long-lived branch in the code repo (alternative)

A long-lived `cairn/<feature>` branch in the code repo holds all CAIRN artifacts. A PR is opened against `main` and **never merged**. The PR is closed when the feature ships and stabilises.

```
my-product (code repo)
├── main                          ← never sees CAIRN artifacts
└── cairn/<feature-slug>          ← long-lived branch
    └── docs/features/<feature>/
        ├── problem-statement.md
        └── ...
```

### How the work flows

1. Create `cairn/<feature-slug>` from `main` in the code repo.
2. Open a PR titled `[CAIRN] <feature> (do not merge)` from this branch to `main`. This is the long-lived PR.
3. Artifacts land on the branch through small sub-PRs targeting the feature branch.
4. Code branches off `main`, merges to `main` per normal flow. Code PRs link to the feature branch's artifacts by URL.
5. AI sessions reach the artifacts via a worktree of the feature branch:
   ```
   git worktree add ../my-repo-cairn cairn/<feature-slug>
   ```
6. When the feature is stable, **close** the PR without merging. The closed PR remains as the historical record. The branch can be deleted.

### When this fits

- You cannot or do not want to spin up a new repo.
- Your team prefers a single-repo workflow and tools that assume it.
- You value the ability to see code and artifacts under the same repo's web UI.

### Tradeoffs you accept

- Discipline cost: no merging is a rule, not a structural fact. Branch protection and clear PR titles help, but humans can override.
- Branch list pollution: the code repo accumulates `cairn/*` branches. Delete on close to keep tidy.
- AI session needs a worktree or sparse fetch to access artifacts from a code branch.
- URL-based references may hit auth friction in some AI tools.

## How to choose between A and B

| Question | If yes, lean toward |
|---|---|
| Can you create a new repo without weeks of process? | A |
| Do you have non-developer stakeholders who need access? | A |
| Have your AI tools struggled with authenticated cross-repo URLs? | A |
| Do you have ten or more teams sharing a few code repos? | A |
| Is your team strongly opinionated about everything-in-one-repo? | B |
| Is repo creation actually painful or impossible in your org? | B |
| Do reviewers strongly value seeing artifacts in the code PR UI? | B |

If most of your answers point to A, pick A. If most point to B, pick B. There is no wrong answer; both honour the underlying principle.

## What both options have in common

- Code is on `main` in the code repo and merges normally.
- CAIRN artifacts never reach the code repo's `main`.
- Artifacts are reviewed before they influence implementation.
- Code PRs reference their story by path or URL.
- AI sessions need access to both code and artifacts; how that happens is the only mechanical difference.

## When neither fits

- **Compliance regimes** that require persistent in-repo documentation. Then merge artifacts into the code repo's `main` under a clearly-archived path and accept the bloat. CAIRN does not require this; it is a fallback for regulated environments.
- **Teams using git platforms that prune closed PRs aggressively.** Verify your platform preserves closed PRs (most do). With option A this concern shifts to the CAIRN repo's history, which is durable.

## A summary you can paste into your team docs

> We use CAIRN. Our artifacts live in [our team's CAIRN repo at <link> | a `cairn/<feature>` branch in our code repo, with a long-lived PR that never merges]. They are reviewed during the build and end when the feature ships. The code repo's `main` never sees CAIRN files. Project-level documentation (system architecture, schema, runbooks, conventions) is out of CAIRN's scope and handled by our existing conventions.
