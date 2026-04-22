# CAIRN

*A calm way to build software with AI, in a team.*

**CAIRN** stands for **C**ontext-driven, **A**rtifact-based, **I**n-repo, **R**eviewed, **N**atural-flow. It is a lightweight methodology for teams who want to use AI as an accelerator without losing control of their codebase, their product, or their people.

> A cairn is a small stack of stones left on a trail so the next person can find the way.
> That is what your docs are for.

## The 60-second version

Most AI development methodologies try to solve the problem by adding more AI: more agents, more personas, more automated handoffs. CAIRN goes the other way. It says:

1. **Write things down.** Problem, scope, architecture, stories. In markdown, in a dedicated CAIRN location (a separate repo or a long-lived feature branch).
2. **Review them like code.** Spec changes go through pull requests. Approvals are the real stage gate.
3. **Let AI read what you already wrote.** Open the CAIRN repo and the code repo together so the AI can cross-reference both.
4. **Skip the personas.** You don't need "Architect Agent" when you have a real architect reviewing a real PR.
5. **End them when the feature ships.** Artifacts were scaffolding for the build; the code is the durable record. Your code repo's `main` stays clean indefinitely.

That is the whole thing. Everything else in this repo is details, templates, and examples.

## Who this is for

- A **team lead** or **delivery manager** who feels AI adoption is getting chaotic and wants a shared way of working.
- A **solo senior engineer** who wants a lightweight shape for their own AI-assisted projects.
- A **company** adopting AI tooling and looking for a process that does not require everyone to use the same IDE.
- **BAs, UX designers, and devs** who want clarity on what they produce and when.

It is probably not for you if you prefer heavy, certifying process frameworks, or if you want the AI to drive the work instead of the humans.

## Where to start

| If you want to... | Read this |
|---|---|
| Understand the philosophy | [MANIFESTO.md](MANIFESTO.md) |
| Know why this exists | [docs/01-why-cairn.md](docs/01-why-cairn.md) |
| See the full lifecycle | [docs/03-lifecycle.md](docs/03-lifecycle.md) |
| See a day in the life | [docs/05-workflow.md](docs/05-workflow.md) |
| Choose where artifacts live | [docs/09-deployment-models.md](docs/09-deployment-models.md) |
| Find your role | [roles/](roles/) |
| Copy a template | [templates/](templates/) |
| See it applied to a real feature | [examples/pub-quiz/](examples/pub-quiz/) |
| Set up a new CAIRN repo for your team | [examples/cairn-repo-starter/](examples/cairn-repo-starter/) |

## Status

This is an opinionated, evolving methodology written by one person based on lived experience. It is not certified, audited, or owned by any company. Take what works, leave what does not.

Author: [Abdullah Siddique](AUTHORS.md)

License: [CC BY 4.0](LICENSE.md). Use it, adapt it, share it; please credit.
