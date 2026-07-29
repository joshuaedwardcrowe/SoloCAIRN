# Contributing to SoloCAIRN

SoloCAIRN is a methodology repo (a fork of [CAIRN](https://github.com/SiddiqueAbdullah/cairn), adapted for a solo maintainer directing AI-assisted/agentic contribution rather than a staffed team) — not a published package. This document is about contributing to *this* repo. It is deliberately separate from what SoloCAIRN itself prescribes for repos that adopt it as their methodology — those are two different questions, and this repo doesn't dictate the answer to the second one for anybody else.

## Before you propose a change

- **Small wording/clarity fixes, typos** — just open a PR.
- **Anything that changes the actual methodology** — a stage's shape, a role, the lifecycle diagram, a template — open an issue first. These changes affect every repo that has adopted SoloCAIRN downstream, so they deserve discussion before the effort goes in.

## Branching & PRs

- Branch off `main`, one branch per change. No long-running branches.
- **PR titles use [Conventional Commits](https://www.conventionalcommits.org/)**: `type(scope): Description` — e.g. `chore(docs): Add Contribution Rules`. `scope` is typically `docs`, since this is a docs-only repo. Unlike KitCli or YnabSharp, there's no changelog-generation or semver pipeline consuming this here — it's used purely for consistency and quick scanning of change type across the ecosystem. Whether a *repo that adopts SoloCAIRN* uses Conventional Commits for its own PRs is still that repo's own decision — SoloCAIRN prescribes this for its own PRs only, not for adopters.
- No enforced CI — there's nothing to build or test, it's markdown.
- Docs-only fixes can be reviewed quickly. Changes to the methodology itself (not just wording) deserve more scrutiny, since they change what every adopting repo is told to do.

## Attribution

SoloCAIRN is released under CC BY 4.0 as a fork of CAIRN (Abdullah Siddique) — see [LICENSE.md](LICENSE.md) and [AUTHORS.md](AUTHORS.md). If your PR introduces a genuinely new idea (not just porting/adapting something CAIRN already had), it should be credited to you in `AUTHORS.md` in the same PR.

## Don't over-deviate from CAIRN

SoloCAIRN forks CAIRN to fix two specific things: the Waterfall-shaped stage-gate/approval structure, and the staffed-team role model. It is not a license to drift from CAIRN's other principles for convenience. If a change isn't in service of "this works for a solo maintainer + AI, not a team" or "gates should be revisable, not frozen," it probably belongs upstream in CAIRN instead, or doesn't belong in either.
