# 09. Deployment models: where the artifacts live

CAIRN artifacts are operationally ephemeral: they are scaffolding for one feature build and stop being load-bearing when the feature ships. They never land on the code repo's `main`. Where they physically live during their short active life is a choice, and the two options are not equally strong.

## The principle (constant either way)

> CAIRN artifacts never land on the code repo's `main`. They scaffold the build, then step out of the way. The code is what survives as the operational truth.

What changes between the two models is the git topology: a separate repo that you treat normally, or a long-lived non-merging branch in the code repo. We recommend the first. The second is a fallback when the first is not possible.

## Option A: separate CAIRN repo (recommended)

A dedicated repo, owned by your team (or your company), holds the CAIRN artifacts. The code repo is left untouched. Devs clone both side by side and open them in the same IDE workspace so AI can cross-reference.

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
2. **Spec PR.** Open a normal PR in the CAIRN repo against its `main`. This PR does merge, into the CAIRN repo's `main`, not the code repo's.
3. **Iterate.** Problem, research, scope, architecture, stories all land on the feature folder via reviewed PRs in the CAIRN repo.
4. **Build.** Code happens on `feat/*` branches off the code repo's `main`, merging to `main` per your team's normal flow. Each code PR description links to the artifact files by path within the CAIRN repo.
5. **Release.** The feature ships and stabilises.
6. **End of life.** When the feature is stable, move its folder from `features/<feature-slug>/` to `archive/<feature-slug>/`, or delete it. Your call. The CAIRN repo's git history is the durable record.

### Why this is the recommended model

- It is structurally sound: a normal repo with normal PRs that merge into normal main. No git anti-patterns. CI, code review, and audit tooling all behave as expected.
- It cleanly decouples artifacts from code, so the code repo stays untouched.
- AI sessions reach the artifacts through filesystem reads, no authenticated URL fetches required.
- Stakeholders can be granted artifact access without code access.

### Costs you do accept (be honest about these)

These are real and the agent who reviews this methodology will catch them. Worth naming up front:

- **CI cannot reach across repos by default.** If you want CI on the code repo to validate that referenced story files exist, you need a cross-repo lookup (a script, a GitHub Action with a token, or similar). Most teams skip this and accept that broken links will be caught at review time.
- **Code review tools cannot show the architecture doc inline with the code PR.** A reviewer looking at a Code PR in GitHub or GitLab cannot see the linked story or architecture by default. The realistic mitigations:
  - The reviewer opens the CAIRN repo in another tab.
  - The PR author quotes the relevant story section in the PR description (a small, deliberate duplication that we accept for review ergonomics; it is not full documentation, just the anchor for the conversation).
  - Some teams add a bot that posts the linked story content as a PR comment automatically; this is tooling, not methodology, but it is a real option.
- **Permissions diverge.** You will end up managing two access lists. This is usually a feature (stakeholders get artifact access without code access) but it is also work.
- **Atomic commits across both are impossible.** You cannot land code and an artifact change in one commit. We argue this is correct, but acknowledge it is a constraint.
- **Two clones, two CIs, two review queues.** The setup tax is real, especially for new joiners. Documenting the two-clone setup in your onboarding is essential.

None of these are dealbreakers. All are real costs to weigh.

### Granularity choice

Three reasonable shapes for the CAIRN repo itself:

| Shape | Best for | Watch out for |
|---|---|---|
| One CAIRN repo per team | Stable teams owning a clear product area | Cross-team discoverability is harder |
| One CAIRN repo per code repo | One code repo serving multiple teams | Harder if a team works across repos |
| One CAIRN repo per company | Cross-team learning, mobile teams | Accumulates fast, needs grooming |

Default to **per team** unless you have a specific reason to choose otherwise.

## Option B: long-lived branch in the code repo (fallback only)

A long-lived `cairn/<feature>` branch in the code repo holds the artifacts. A PR is opened against `main` and never merged. The PR is closed when the feature ships and stabilises.

> **Honest warning.** This pattern uses git in a way some senior engineers and most audit tools will treat as suspicious. A long-lived PR that closes without merging is structurally indistinguishable from a rejected PR; reporting tools and process metrics may misclassify your shipped work as abandoned. Use this option only if you genuinely cannot create a separate CAIRN repo.

```
my-product (code repo)
├── main                          ← never sees CAIRN artifacts
└── cairn/<feature-slug>          ← long-lived branch
    └── features/<feature>/
        ├── problem-statement.md
        └── ...
```

### How the work flows

1. Create `cairn/<feature-slug>` from `main` in the code repo.
2. Open a PR titled `[CAIRN] <feature> (do not merge)` from this branch to `main`. Pin or label it clearly so reviewers and audit tools know what it is.
3. Artifacts land on the branch through small sub-PRs targeting the feature branch.
4. Code branches off `main`, merges to `main` per normal flow. Code PRs link to the feature branch's artifacts by URL.
5. AI sessions reach the artifacts via a worktree of the feature branch:
   ```
   git worktree add ../my-product-cairn cairn/<feature-slug>
   ```
6. When the feature is stable, **close** the PR without merging. The closed PR remains as the historical record. The branch can be deleted.

### When this might fit

- You genuinely cannot spin up a separate repo (corporate policy, slow process, hard limits).
- You explicitly value seeing artifacts in the same web UI as code, more than you mind the git anti-pattern smell.

### Tradeoffs you accept

- **Anti-pattern smell.** Long-lived non-merging PRs look wrong to anyone who has not been told about CAIRN. Expect to explain this to every new joiner and every external reviewer.
- **Audit and metrics confusion.** Closed-without-merge PRs may show up as "rejected" in your team's reporting tools. Either configure those tools to ignore CAIRN PRs, or accept the noise.
- **Discipline cost.** Not merging is a rule, not a structural fact. Branch protection and clear PR titles help, but humans can override.
- **Branch list pollution.** The code repo accumulates `cairn/*` branches. Delete on close to keep tidy.
- **AI session needs a worktree or sparse fetch** to access artifacts from a code branch.
- **URL-based references may hit auth friction** in some AI tools.

## How to choose

For most teams, **pick Option A**. The structural soundness wins.

Pick Option B only if:

- Repo creation in your organisation is genuinely difficult and not worth the political cost, **and**
- Your team is comfortable explaining the long-lived non-merging PR pattern to anyone who notices it.

If you find yourself rationalising Option B, push harder on getting a new repo first.

## What both options have in common

- Code is on `main` in the code repo and merges normally.
- CAIRN artifacts never reach the code repo's `main`.
- Artifacts are reviewed before they influence implementation.
- Code PRs reference their story by path or URL.
- AI sessions need access to both code and artifacts; how that happens is the mechanical difference.

## When neither fits

- **Compliance regimes** that require persistent in-repo documentation. Then merge artifacts into the code repo's `main` under a clearly-archived path and accept the bloat. CAIRN does not require this; it is a fallback for regulated environments.
- **Teams using git platforms that prune closed PRs aggressively.** Verify your platform preserves closed PRs (most do). With Option A this concern shifts to the CAIRN repo's history, which is durable.

## A summary you can paste into your team docs

> We use CAIRN. Our artifacts live in our team's CAIRN repo at `<link>` (recommended), or alternatively on a `cairn/<feature>` branch in our code repo with a long-lived PR that never merges (fallback). They are reviewed during the build and end when the feature ships. The code repo's `main` never sees CAIRN files. Project-level documentation (system architecture, schema, runbooks, conventions) is out of CAIRN's scope and handled by our existing conventions; see [docs/10-what-cairn-does-not-solve.md](10-what-cairn-does-not-solve.md).
