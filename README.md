<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="logos/cairn-logo-dark.svg">
    <img alt="CAIRN" src="logos/cairn-logo-light.svg" width="340">
  </picture>
</p>

<p align="center"><strong>AI as accelerator, not author.</strong></p>

# CAIRN

**CAIRN** stands for **C**ontext-driven, **A**rtifact-based, **I**n-repo, **R**eviewed, **N**atural-flow. It is a lightweight methodology for teams who want to use AI as an accelerator without losing control of their codebase, their product, or their people.

> A cairn is a small stack of stones left on a trail so the next person can find the way.
> That is what your docs are for.

## The 60-second version

Most AI development methodologies try to solve the problem by adding more AI: more agents, more personas, more automated handoffs. CAIRN goes the other way. It says:

1. **Write things down.** Problem, scope, architecture, stories. In markdown, in a dedicated CAIRN location (a separate repo or a long-lived feature branch).
2. **Review them like code.** Spec changes go through pull requests. Approvals are the real stage gate.
3. **Let AI read what you already wrote.** Open the CAIRN repo and the code repo together so the AI can cross-reference both.
4. **Skip the personas.** You don't need "Architect Agent" when you have a real architect reviewing a real PR.
5. **End them when the feature ships.** Artifacts were scaffolding for the build; the code is the **operational truth** from then on. Your code repo's `main` stays clean indefinitely. The CAIRN repo's git history (or the closed PR) remains as a **historical record** if you ever need to look back.

That is the whole thing. Everything else in this repo is details, templates, and examples.

## What CAIRN claims

With AI as an accelerator, the cost of producing reviewed, shared context for a feature build has collapsed. The discipline that was "too expensive to do consistently" is no longer expensive. Teams that internalise this ship more coherent work, and the coordination wins compound. CAIRN is the small set of habits that captures most of that benefit.

CAIRN is scoped to the build phase of one feature in an AI-assisted team. It is not a transformation programme, and it deliberately does not own project-level docs, on-call, prioritisation, or long-horizon institutional knowledge. See [docs/10-what-cairn-does-not-solve.md](docs/10-what-cairn-does-not-solve.md) for the honest boundary.

## Who this is for

- A **team lead** or **delivery manager** who feels AI adoption is getting chaotic and wants a shared way of working.
- A **solo senior engineer** who wants a lightweight shape for their own AI-assisted projects.
- A **company** adopting AI tooling and looking for a process that does not require everyone to use the same IDE.
- **BAs, UX designers, and devs** who want clarity on what they produce and when.

CAIRN is not for you if you want a heavy, certifying process framework, or if you want AI to drive the work instead of the humans. Pick something else.

## Where to start

| If you want to... | Read this |
|---|---|
| Understand the philosophy | [MANIFESTO.md](MANIFESTO.md) |
| Know why this exists | [docs/01-why-cairn.md](docs/01-why-cairn.md) |
| See the full lifecycle | [docs/03-lifecycle.md](docs/03-lifecycle.md) |
| See a day in the life | [docs/05-workflow.md](docs/05-workflow.md) |
| Choose where artifacts live | [docs/09-deployment-models.md](docs/09-deployment-models.md) |
| Know what CAIRN does not solve | [docs/10-what-cairn-does-not-solve.md](docs/10-what-cairn-does-not-solve.md) |
| Find your role | [roles/](roles/) |
| Copy a template | [templates/](templates/) |
| See it applied to a real feature | [examples/pub-quiz/](examples/pub-quiz/) |
| Set up a new CAIRN repo for your team | [examples/cairn-repo-starter/](examples/cairn-repo-starter/) |

## Author and license

By [Abdullah Siddique](AUTHORS.md). Released under [CC BY 4.0](LICENSE.md): use it, adapt it, share it, credit the author.

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="logos/cairn-logo-dark-sm.svg">
    <img alt="CAIRN" src="logos/cairn-logo-light-sm.svg" width="106">
  </picture>
</p>
