# Role: Maintainer

You are every thread CAIRN used to split across a Team Lead, a Business Analyst, a UX Designer, and QA. In SoloCAIRN, you talk to whoever has the problem (or research it yourself), decide what is worth building, sketch how it should work, write it all down, and decide when it is actually done. You do not have specialists to hand any of this to — that is the whole premise of this role.

## Who you are

- You hold the entire lifecycle from Discovery through Operate, except Build (see [Contributor](contributor.md)).
- You are your own skeptic: nobody else is going to ask "is this actually the right problem" or "did we test the edges" unless you build the habit of asking yourself.
- You care about the shape of the work as much as the content, because there is no one else watching the shape.
- You know when to slow down and write something down properly, and when a two-line issue is enough (see [principle 7, small is beautiful](../MANIFESTO.md)).

## Artifacts you own

- `problem-statement.md`, `stakeholder-interviews.md` (or informal notes, if there's no one to formally interview) — Discovery. Draw on the [Business Analysis](../skills/business-analyst.md) skill.
- `ux-research.md` or equivalent notes — Research, when it's worth doing at all for the size of the work. Draw on [UX Design / Research](../skills/ux-designer.md).
- `scope.md`, `open-questions.md` — Scope.
- `architecture.md` — Design, when the work is big enough to need one. [UX Design / Research](../skills/ux-designer.md) applies here too for UX patterns.
- Stories (or GitHub Issues — see [SoloCAIRN's Breakdown stage](../docs/03-lifecycle.md) on artifact form) — Breakdown.
- `qa-checklist.md` and retro notes — Review and Operate. Draw on the [QA](../skills/qa.md) skill.

## Artifacts you contribute to

- Code PRs, when you're the one reviewing a Contributor's work (see [Contributor](contributor.md) on what review actually looks like without a dedicated second reviewer).

## How AI fits your work

- **Drafting from notes.** A rough page of bullets becomes a 200-word problem statement, a scope doc, or a story breakdown in one prompt. You edit it into the real thing.
- **Playing the specialist you don't have.** Ask AI to review a flow for accessibility gaps, or a story for missing edge cases, the way a UX Designer or QA would have. Treat it as a starter checklist, not gospel — but it's a genuinely useful substitute when there's no human specialist to catch these instead.
- **Consistency checks.** Ask AI to check the scope against the stories and flag missing or contradictory items — the cross-checking a team would do informally in conversation.
- **Retro summaries.** Feed it the period's PR list and ask for themes.

## How AI does not help

- It does not talk to your users. If Discovery/Research needs real conversations, that's still your job.
- It does not have your judgment about what's actually worth building. It drafts; you decide.
- It will happily play every specialist role at once and sound confident doing it — which is exactly when you need to slow down and check its work, not speed up.

## Anti-patterns for this role

- **Skipping stages because "it's just me."** The stages exist because each question (is this the right problem? what's in scope? how should this work? is it actually done?) is real, not because a team happened to need separate people to ask them. Compress the ceremony, not the questions.
- **Never writing anything down because "I'll remember."** You won't, in six months, and neither will the intermittent contributor who picks this up next (see [principle 12](../MANIFESTO.md)).
- **Doing everything yourself out of habit even when a Contributor is available.** If someone's picked up a story, let them own the Build stage — don't quietly redo their work.

## A day in the life

**Morning.** A support message surfaces a real problem. Sketch a one-paragraph problem statement. Ask AI to draft it properly from your notes; edit it into the real thing.

**Midday.** Decide what's actually in scope for this round. Open the issue (idea-stage title, per the issue-title convention). If it's small, that's the whole Scope step — move straight to Breakdown.

**Afternoon.** Break it into one or two tickets. If a Contributor is around, hand one off. If not, pick it up yourself later.

**End of day.** Review whatever Code PR landed today. Update the checklist or close the loop.

## The hidden job

Your hidden job is to be your own dissenting voice — the BA who asks "why," the UX Designer who protects the user, the QA who won't sign off on theatre. Nobody else is going to do it for you. That discipline, not any specific artifact, is what makes this role work without a team behind it.
