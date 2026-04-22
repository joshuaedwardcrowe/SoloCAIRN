# CAIRN repo starter

This folder shows what a brand-new **CAIRN repo** should look like on day one if you choose the separate-repo deployment model (see [docs/09-deployment-models.md](../../docs/09-deployment-models.md)).

It is a starting shape, not a strict structure. Adapt freely.

## What is in here

- [example-repo-readme.md](example-repo-readme.md): the file you would copy into your new CAIRN repo as its top-level `README.md`.
- This `README.md`: meta-explanation, do not copy.

## How to set up your team's CAIRN repo

1. **Create a new git repo** on your platform of choice. Name it something like `<team>-cairn` or `<product>-cairn`.
2. **Add a top-level README.** Use [example-repo-readme.md](example-repo-readme.md) as a starting point, fill in your team's specifics.
3. **Create the folder structure:**
   ```
   <team>-cairn/
   ├── README.md             ← from the template above
   ├── features/             ← active features (one folder each)
   └── archive/              ← shipped features (optional, can also delete)
   ```
4. **Set permissions.** Decide who can read, who can write, who can review PRs. Stakeholders, BAs, UX, and devs typically all need at least read.
5. **Tell your team.** Share the URL. Add a pointer from the code repo's `CLAUDE.md` (or equivalent) so AI sessions know where the artifacts live.
6. **Start your first feature.** Create `features/<first-feature-slug>/` and open a CAIRN PR with the problem statement.

## When to archive vs delete

Both are valid:

- **Archive**: move shipped features to `archive/<feature-slug>/`. Keeps everything searchable. Useful if your team values "have we done this before?" lookups.
- **Delete**: remove the folder entirely when the feature ships and stabilises. The git history preserves it. Cleaner working tree, but slightly worse for casual browsing.

Pick one and apply consistently. Mixing them is the worst option.

## What the repo grows into

After a few months of use:

```
<team>-cairn/
├── README.md
├── features/
│   ├── pub-quiz-live-scoring/      ← active
│   │   ├── problem-statement.md
│   │   ├── stakeholder-interviews.md
│   │   ├── ux-research.md
│   │   ├── scope.md
│   │   ├── architecture.md
│   │   ├── open-questions.md
│   │   ├── qa-checklist.md
│   │   └── stories/
│   │       ├── backend/
│   │       ├── frontend/
│   │       ├── mobile/
│   │       └── database/
│   └── new-onboarding-flow/        ← active
│       └── ...
└── archive/
    ├── 2026-q1-bulk-export/
    │   ├── problem-statement.md
    │   ├── scope.md
    │   ├── architecture.md
    │   ├── retro.md
    │   └── ...
    └── 2026-q1-account-deletion/
        └── ...
```

The shape is consistent across features. New devs and AI sessions both benefit from the predictability.
