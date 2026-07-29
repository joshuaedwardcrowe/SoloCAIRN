# 11. The four homes for a piece of process

If you run SoloCAIRN alongside a personal context store (something [MyBrain](https://abdullah-compendium.vercel.app/mybrain)-shaped — externalized markdown, git-backed, read by your AI sessions), you'll keep hitting the same question: where does this specific rule, convention, or decision actually belong? There are four distinct homes. The recurring mistake is collapsing two of them into one.

## The four homes

1. **CAIRN** (or whatever upstream methodology you forked SoloCAIRN from) — universal to *any staffed team*, not solo-specific.
2. **SoloCAIRN** (this fork) — universal to *any solo maintainer* doing AI-assisted work, not specific to your own personal taste.
3. **Your personal context store** — your own preferences and working style. Not binding on anyone else, including other contributors to your own repos.
4. **Each individual repo's own `CONTRIBUTING.md`** — the actual binding, shared contract for anyone (including you) contributing to that specific repo. This applies per-repo, not per-"everything you maintain" — and an org meant to operate as its own independent simulated organization gets its own infrastructure (its own Ideas/backlog board, its own `CONTRIBUTING.md`), not your personal-account one, even though you own or run it. Repos under your own personal account that aren't simulated orgs can reasonably share personal-account infrastructure.

## The test

- Would this apply to any team, anywhere? → **Upstream CAIRN.**
- Any solo maintainer, not just you? → **SoloCAIRN.**
- Is it genuinely just how you personally like to work, not something another contributor needs to follow? → **Your personal context store.**
- Does it need to be binding for anyone contributing to *this specific repo/org*? → **That repo's own `CONTRIBUTING.md`** — and if the org is a simulated independent organization, its own boards/infra too, not your personal ones.

## Why this matters

The mistakes are always the same shape — collapsing two of the four homes into one:

- A repo-specific extension nearly gets written into SoloCAIRN itself, as if every solo maintainer wants it, when it's really one repo's own adopted choice.
- A binding contributor rule nearly gets left only in a personal context store, where other contributors — human or a fresh AI session working on that repo — will never see it.
- A sub-organization's own planning infrastructure (its ideas backlog, its own boards) nearly gets folded into a personal account's, mixing two unrelated bodies of work on one undifferentiated list.
- Even the general methodology you bring to every project (how you estimate, how you plan) can get *under*-shared if it's left only in your personal context store instead of also landing in the specific repos it actually governs.

## How to apply

Before writing any process or convention down, explicitly run it through the four-way test above rather than defaulting to "put it wherever feels closest." When in doubt, surface the ambiguity out loud rather than picking one silently — most of these mistakes only get caught after the fact, by someone noticing the wrong placement, not by the test being applied up front. Applying it up front is cheaper.
