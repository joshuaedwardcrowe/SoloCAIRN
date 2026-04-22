# 10. What CAIRN does not solve

CAIRN is a methodology for building one feature with a team and with AI as an accelerator. It is deliberately scoped to that. This doc names the things we explicitly do not address, why, and where to look for answers instead.

The reason this matters: a methodology that pretends to solve everything solves nothing. Most "agile" frameworks failed by overreaching. CAIRN is honest about its boundary.

## The things CAIRN is silent about

### 1. Project-level documentation

System-level architecture as it currently stands. Schema as it is currently deployed. Conventions and standards. The project's AI context file (CLAUDE.md, .cursor/rules, etc.). Repo-wide checklists.

**Why we are silent.** These are different artifacts with a different lifecycle (durable, evolving, owned by the project rather than any one feature). Mixing them with feature scaffolding produces a methodology that is either too heavy for features or too thin for the project. We picked the feature-scoped lane.

**What to do instead.** Your team or your company decides where these live and how they are maintained. Common patterns: a top-level `docs/` folder on the code repo's `main`, a wiki, a separate documentation repo. Whatever you choose, treat them as durable, not ephemeral.

### 2. Onboarding and codebase orientation

How a new joiner gets up to speed on an unfamiliar system. How they learn the shape of the code, the team's conventions, the operational quirks.

**Why we are silent.** Onboarding draws on durable artifacts (architecture docs, runbooks, conventions) more than on feature-scoped ones. A new joiner reading last quarter's spec for a shipped feature learns history; reading the current architecture learns the system. CAIRN provides the former, not the latter.

**What to do instead.** Maintain a project-level onboarding doc. Pair new joiners with experienced ones. Keep your AI context file genuinely current.

### 3. Production debugging and operations

How you respond when production breaks. How you investigate an alert at 2am. Postmortems. Incident tracking.

**Why we are silent.** Operational work pulls from runbooks, dashboards, logs, and the live system. It does not need a feature spec. Bolting incident response onto a feature methodology would dilute both.

**What to do instead.** Maintain runbooks for services you own. Have an incident process. Write postmortems and keep them somewhere durable. None of this is CAIRN, all of this is important.

### 4. Killing or pivoting features

Deciding which of three half-finished features to drop. Reshaping a feature mid-flight when reality changes. Reallocating effort when a stakeholder pulls funding.

**Why we are silent.** These are organisational and product decisions, not methodology questions. CAIRN gives you the artifacts to think clearly about a feature; it does not tell you whether the feature should exist.

**What to do instead.** Trust your team lead, BA, and product judgment. Use the open-questions doc to track existential doubts about a feature. Be willing to close a Spec PR without ever building anything; that is a CAIRN success, not a failure.

### 5. Maintaining shared understanding over years

How a team that has shipped 200 features keeps a coherent mental model of the product. How institutional knowledge survives turnover.

**Why we are silent.** This is a long-horizon problem. CAIRN's artifacts are short-horizon by design. Asking CAIRN to solve multi-year coherence is like asking a sprint planning tool to solve company strategy.

**What to do instead.** Invest in your project-level docs. Run regular architecture reviews. Treat your AI context file as living memory. Conduct cross-team learning sessions. None of this is CAIRN.

### 6. Cost modelling and prioritisation

Whether a feature is worth its cost. Which features to do first. ROI, budgets, capacity planning.

**Why we are silent.** Prioritisation is a product and business function, not a methodology one. CAIRN can produce the artifacts that inform a prioritisation decision (a problem statement, a scope, a rough effort estimate from breaking down stories), but the decision itself sits elsewhere.

**What to do instead.** Use whatever prioritisation framework your organisation runs (RICE, ICE, OKRs, gut). CAIRN is compatible with all of them.

### 7. Cross-team coordination at scale

How ten teams sharing infrastructure agree on direction. How dependencies between teams get resolved. Architecture review boards.

**Why we are silent.** This is org design, not methodology. CAIRN works fine inside one team; it does not impose on cross-team structures.

**What to do instead.** Use your existing org mechanisms (planning forums, architecture councils, dependency tracking tools). CAIRN's per-team CAIRN repo is searchable enough that adjacent teams can read each other's work, but discovery and coordination still require human effort.

### 8. AI tool selection and governance

Which AI assistant your team should use. How to evaluate one against another. How to keep AI usage compliant with company policy.

**Why we are silent.** Tooling decisions and governance vary by company and change quickly. A methodology that named specific tools would age badly.

**What to do instead.** Your CISO, your platform team, and your team lead decide. CAIRN works with any AI assistant capable of reading markdown and writing code; the artifacts are the constant.

## The honest summary

CAIRN handles the feature build. That is genuinely useful and not nothing. But:

- If your team's main pain is **rotting project docs**, CAIRN will not fix it. Fix that separately.
- If your main pain is **production reliability**, CAIRN will not fix it. Invest in runbooks and operational practice.
- If your main pain is **deciding what to build**, CAIRN will help you think clearly once you have decided, but the decision itself is yours.
- If your main pain is **getting new joiners productive**, CAIRN will help only at the edges. Project-level docs and pairing matter more.

A skeptical reader is right to point out that the build phase is the part of software delivery teams already know how to do reasonably well, when they care to. CAIRN's claim is that AI changes the economics of doing it well consistently, and that the team-coordination wins compound. That is the claim. Take it for what it is.

## Where this puts CAIRN in the toolbox

Think of CAIRN as one tool, not the whole toolbox. The other tools you need:

- A way to maintain durable project docs.
- A way to onboard new people.
- A way to operate the system you have built.
- A way to decide what to build next.
- A way to govern your tooling and AI usage.

CAIRN does not replace any of them. It makes the build phase more coherent, especially in an AI-assisted team. That is the whole pitch.
