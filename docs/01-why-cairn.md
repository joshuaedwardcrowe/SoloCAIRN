# 01. Why ACAIRN exists

## The current landscape

Look at a typical team adopting AI for development right now. You will see one of three patterns:

**Pattern A: Every person for themselves.**
Everyone uses Copilot or Claude or Cursor or whichever tool they like. They prompt differently. They keep context in their own heads or private notes. Outputs vary wildly. Code review reveals that two developers built incompatible pieces because nobody wrote the design down. Senior engineers quietly do more prompting work than the juniors and get no credit.

**Pattern B: The persona framework.**
Someone discovers a methodology that promises an "AI-driven" lifecycle: agents with names and personalities, simulated handoffs, multi-phase workflows. It looks impressive in a demo. In practice, people spend more time tending to the framework than shipping. The personas do not behave like specialists, they behave like the same model wearing different costumes.

**Pattern C: Ban it entirely.**
Leadership is spooked. AI is off-limits. The best engineers use it anyway on personal machines, but cannot tell anyone, so the knowledge does not spread. You lose the productivity gains *and* the shared learning.

ACAIRN is what happens when you refuse all three options and ask what teams actually need.

## What teams actually need

Talk to any team lead who is one year into AI adoption and they will tell you some version of the same thing:

> "I don't need more AI. I need my team to agree on what we're building before they start, and I need the AI sessions to share that context."

This is not a tooling problem. It is a coordination problem. And coordination problems have well-known solutions: shared artifacts, reviewed decisions, clear ownership. These were the answers before AI and they are still the answers.

What AI changes is not the need for coordination. It changes the **cost of producing artifacts**. A problem statement that used to take two days to draft takes half an hour. An architecture sketch that used to live in a whiteboard photo can be a proper markdown document without anyone resenting the writing time.

That shifts the economics. In a world where writing a spec was expensive, teams learned to skip it. In a world where writing a spec is cheap, skipping it is a choice, and usually a bad one.

## The insight

Here is the thing most AI methodologies miss:

> The AI is not the bottleneck. The humans are the bottleneck. The AI is the opportunity.

If you give an AI a vague prompt and a messy repo, you get vague, messy output at high speed. If you give it a clear problem, a reviewed architecture, and a well-scoped story, you get surprisingly good work in minutes. The difference is context, and context is a human-produced artifact.

So ACAIRN inverts the usual question. Instead of asking *"how do we make the AI smarter?"* it asks:

> *"How do we make sure every AI session on our team starts from the same, reviewed, high-quality context?"*

The answer turns out to be unglamorous: write things down in a place that is not your code repo's `main` (a separate ACAIRN repo, recommended), review them like code, and end them when the feature ships.

## Why "ACAIRN"

A cairn is a small pile of stones that hikers leave on a trail to mark the way for those who come next. It is not a signpost installed by an authority. It is a modest, hand-built marker that says *someone has been here, this is the path, keep going*.

That is the spirit of the method. Every artifact you write is a stone on the trail. For your teammates, for the AI, for future you. None of them replaces the walk. But together they turn "which way do I go?" into "I see the cairn, I know where to step next."

## What ACAIRN is not

- **Not a framework.** There is no CLI to install, no config file, no runtime.
- **Not a certification.** There are no certified ACAIRN practitioners. Please do not invent them.
- **Not a replacement for judgment.** It tells you what artifacts to produce and when. It does not tell you what to put in them.
- **Not universally right.** It works best for teams of 3 to 15 on product-shaped work. Regulated environments, research spikes, and ten-person monoliths probably need different things.

## What to read next

- If you want the principles behind the method: [02-philosophy.md](02-philosophy.md)
- If you want to see where the method fits in your week: [05-workflow.md](05-workflow.md)
- If you are ready to roll it out: [08-adoption.md](08-adoption.md)
