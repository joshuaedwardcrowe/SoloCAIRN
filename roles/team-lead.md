# Role: Team Lead / Delivery Manager

You are the person who holds the thread. In SoloCAIRN, you are the connective tissue between stakeholders, BAs, UX, and devs. You do not write every artifact, but you make sure they get written, reviewed, and merged.

## Who you are

- You open most Spec PRs and most Story PRs.
- You facilitate reviews, but you do not do them all yourself.
- You are the default owner of anything that falls between other roles.
- You care about the shape of the work as much as the content.

## Artifacts you own

- `scope.md`: you draft it, stakeholders review it, the team approves it.
- `open-questions.md`: you keep it alive and chase owners.
- `architecture.md`: for small features. For big ones, you facilitate while specialists contribute.
- Stories in `features/<feature>/stories/`: you draft the breakdown, devs refine their own.
- Retro docs: you capture them after each feature ships.

## Artifacts you contribute to

- Problem statements: you review what the BA drafts.
- UX research: you review and push back on scope creep.
- Code PRs: you review where your attention is needed, not where it is routine.

## How AI fits your work

- **Drafting Spec PRs at speed.** Paste a transcript of a stakeholder call, ask AI to produce a problem-statement draft. You edit it into the real thing.
- **Breaking down stories.** Give AI the scope and architecture docs; ask for a proposed breakdown into per-platform stories. Review carefully.
- **Chasing consistency.** Ask AI to check the scope against the stories and flag missing or contradictory items.
- **Retro summaries.** Feed AI the week's PR list and ask for themes.

## Anti-patterns for this role

- **Owning everything.** You are a facilitator, not a bottleneck. Push ownership to the right specialist.
- **Approving to keep velocity.** Your approval is a decision. Take it seriously. Velocity at the cost of quality is not velocity.
- **Becoming the only person who writes specs.** The team learns by doing. Rotate the Spec PR authorship.
- **Skipping the retro because things went fine.** A retro after a successful feature is where you learn what actually worked.

## A day in the life

**Monday.** Review weekend PRs. Open a Spec PR for next week's feature. Stub in problem and scope. Tag the BA to fill in the details.

**Tuesday.** Pair with UX on the research doc. Update `open-questions.md` from the morning stakeholder call.

**Wednesday.** Facilitate the design conversation. Take notes, turn them into `architecture.md`, open an SoloCAIRN PR (or push to the long-lived branch in the branch model).

**Thursday.** Break the feature into stories. Open a Story PR. Tag the devs for review.

**Friday.** Approve the Story PR after changes. Kick off the first Code PRs. Do a retro on last week's shipped feature.

## The hidden job

The hidden job of the team lead in SoloCAIRN is to notice when the method is not serving the team, and to change it. The templates in this repo are a starting point. Your job is to evolve them until they fit your team, and to protect the team from adopting ceremony that does not earn its keep.
