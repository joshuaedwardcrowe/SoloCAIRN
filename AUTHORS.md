<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="logos/cairn-logo-dark-sm.svg">
    <img alt="SoloCAIRN" src="logos/cairn-logo-light-sm.svg" width="106">
  </picture>
</p>

# Authors

## Abdullah Siddique

CAIRN, the methodology SoloCAIRN is forked from, was created and is maintained by **Abdullah Siddique**: https://github.com/SiddiqueAbdullah/cairn.

It grew out of practical work on multi-service projects where AI was being adopted unevenly across a team, and where the usual answers (more agents, more personas, more automated handoffs) were making things worse instead of better. The method is the shape that actually stuck: feature-scoped artifacts in markdown, reviewed like code, kept off the code repo's `main`, with humans owning the decisions.

## Joshua Crowe

**SoloCAIRN** is Joshua Crowe's fork of CAIRN, scoped to a solo maintainer (optionally directing AI-assisted/agentic contribution) plus occasional intermittent external contributors — not a staffed team. Two distinct problems drive the fork:

1. CAIRN's stage-gated, artifact-approval shape leans Waterfall in places (design fully decided before breakdown and build; approval framed as a one-time gate; no built-in loop back into a feature's own Design/Scope once Build reveals something new). SoloCAIRN keeps CAIRN's core insight (externalise context, review it like code) while making artifacts revisable by default and adding an explicit intra-feature feedback loop.
2. CAIRN's role model (Team Lead, Business Analyst, UX Designer, QA, per-platform devs) assumes people to distribute stage-ownership across. There usually aren't any here — this is still an open restructuring, not yet done. If you have a staffed team with those roles, upstream CAIRN already serves that case well; use it directly rather than this fork.

## Influence and prior art

CAIRN borrows ideas from a lot of places and invents very few. Honest credits:

- **Agile**, for the habit of small stories and short cycles.
- **Lean**, for the habit of questioning every artifact that does not earn its keep.
- **BMAD-METHOD**, for naming the problem clearly and mapping the full lifecycle, even though CAIRN disagrees with its approach to personas.
- **Conventional code review**, for the insight that the best quality gate is a second pair of eyes.
- Every team the author has worked with that tried, succeeded, or failed to make AI-assisted development feel sane.

## License and contributing

SoloCAIRN is released under [CC BY 4.0](LICENSE.md), same as upstream CAIRN. You may use, adapt, and share it freely; please credit both Abdullah Siddique (original CAIRN methodology) and Joshua Crowe (SoloCAIRN adaptations), and link back to both.

This repo is maintained personally, intermittently, and as open source — issues and pull requests from anyone are welcome. Substantial forks and adaptations for your own organisation are encouraged: take the shape, make it yours, keep the attribution.

## Contact

Joshua Crowe (SoloCAIRN) · Abdullah Siddique (original CAIRN)

Reach out if you are adopting SoloCAIRN for your own solo/AI-assisted project and want to compare notes.
