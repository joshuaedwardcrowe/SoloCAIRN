# Role: Business Analyst

You are the bridge between the people with the problem and the people building the solution. In SoloCAIRN, your work is how the team learns what is actually going on before anyone writes code.

## Who you are

- You spend real time with stakeholders, customers, and support channels.
- You turn messy human conversations into structured artifacts.
- You are often the first to notice that the "obvious" solution is wrong.
- You are a skeptic in a good way: you keep asking *why*.

## Artifacts you own

- `problem-statement.md`: the canonical statement of what is wrong and for whom.
- `stakeholder-interviews.md`: structured notes from conversations.
- `open-questions.md`: you are often the first to add items here.

## Artifacts you contribute to

- `ux-research.md`: you feed raw observations to UX, and co-author themes.
- `scope.md`: you push back when scope drifts away from the actual problem.
- Stories: you review stories to confirm they serve the original problem.

## How AI fits your work

- **Interview transcription and summarisation.** Record with permission, feed the transcript to AI, get a clean summary. You check, clean, and write the final version. This is the single biggest AI win for BAs.
- **Theme extraction.** Across ten interviews, AI can cluster what people said. You validate the clustering and name the themes.
- **Drafting problem statements from notes.** A rough page of bullets becomes a 200-word problem statement in one prompt.
- **Finding contradictions.** Ask AI to compare two interviews and flag where people disagree.

## How AI does not help

- It does not sit in the room. It does not hear the pause before someone answers.
- It does not know which stakeholders are the loudest and which are the most credible.
- It will invent user needs that were not expressed if you prompt it imprecisely. Always ground it in actual quotes or notes.
- It does not replace the interview. The interview is still the job.

## Anti-patterns for this role

- **Confusing quantity with quality.** Ten shallow interviews are worse than three deep ones.
- **Letting AI write the problem statement from thin air.** If your problem statement is not grounded in actual stakeholder input, it is a hypothesis, not a statement.
- **Over-summarising.** Rich quotes are more useful than smooth summaries. Keep some of the original voice.
- **Solving in the problem statement.** If the doc proposes a solution, it is not a problem statement.

## A day in the life

**Morning.** Two stakeholder calls, back to back. Recorded with permission. Sparse notes during the call, so you can listen.

**After the calls.** Feed transcripts to AI, ask for a themed summary. Read the summary. Edit it. Where the AI paraphrased something meaningful, replace it with the original quote.

**Midday.** Open an SoloCAIRN PR adding the interview notes to the feature folder (or push to the long-lived branch in the branch model). Comment in the PR on anything the team should know.

**Afternoon.** Update `open-questions.md` with three new questions. Assign two to yourself; one to the Team Lead.

**End of day.** Pair with UX on one theme that feels important. Decide whether it changes the scope.

## The hidden job

Your hidden job is to hold the team accountable to the actual problem. When the team drifts into building something clever but misaligned with stakeholder needs, you are the one who notices. That noticing is the whole point of the role. Protect it from being automated away.
