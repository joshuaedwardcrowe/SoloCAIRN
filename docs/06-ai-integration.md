# 06. How AI fits in

CAIRN is designed so that any AI assistant (Claude, Cursor, Copilot, others) can plug in and be immediately useful, because the context it needs is already in the repo. This doc explains how to make that work in practice.

## The mental model

Think of AI as a very fast, very literate, context-free new hire. It reads whatever you put in front of it. It writes whatever you ask it to. It has no opinions of its own that survive the next prompt. It remembers nothing between sessions unless you write it down.

Given that model, two things follow:

1. **The quality of its output is almost entirely determined by the quality of the context you provide.**
2. **Its output should always be reviewed by a human before it influences reality.**

Everything else in this doc is a consequence of those two rules.

## Set up the repo for AI

### The root AI context file

Most AI tools look for a well-known file at the repo root. Claude Code looks for `CLAUDE.md`. Cursor uses `.cursor/rules/`. Copilot uses `.github/copilot-instructions.md`. Pick whichever is relevant to your team and fill it with:

- **What this project is.** Two sentences.
- **The tech stack.** Languages, frameworks, key libraries.
- **The directory layout.** Where things live.
- **The conventions.** Style, naming, testing expectations, commit message format.
- **What to never do.** Don't touch the generated schema files. Don't modify vendored code. Don't run migrations locally.
- **Where to find more context.** Pointers to `docs/` and `tasks/`.

Keep it short. Thousands of lines will be ignored or skimmed. Hundreds is the sweet spot.

See [templates/CLAUDE.md.example](../templates/CLAUDE.md.example) for a starting point.

### Per-feature context

When working on a feature, the AI should naturally encounter:

- `docs/features/<feature>/problem-statement.md`
- `docs/features/<feature>/architecture.md`
- `tasks/<platform>/STORY-XX.md`

These files teach it what is being built and why. You do not need to paste them into prompts, because they are in the repo and the tool can read them.

### Subagents and task-scoped context

Advanced AI tools offer subagents or task runners. Use them for:

- **Exploration.** "Find all places that use the session service." Subagent returns results, your main session stays focused.
- **Planning.** "Plan the implementation of this story." Subagent produces a plan, you review, then implement.
- **Review.** "Review this diff against the story's acceptance criteria." Subagent drafts, you decide.

Subagents give you context isolation without personas. They are the mechanism that actually delivers the promised benefit of multi-agent frameworks.

## Prompting patterns

### Good prompts name the artifact

**Weak.** "Build the login page."

**Strong.** "Implement the login page per `tasks/frontend/AUTH-03-login-page.md`. Follow the design in `docs/features/auth/ux/login.png`. Use the conventions in `CLAUDE.md`."

The strong prompt does no extra work that the repo cannot do. The AI reads the story, the design, and the conventions, and proceeds.

### Good prompts ask for the plan first

**Weak.** "Do the thing."

**Strong.** "Before you change any code, show me your plan for implementing this story, including which files you will touch and in what order."

Plans are cheap to review. Code is not. Make AI spend your time on the plan, not the retry.

### Good prompts name constraints

**Weak.** "Write a test."

**Strong.** "Write an integration test that uses the real database, not a mock. See `CLAUDE.md` for why we avoid mocks here."

### Good prompts end with "what did you skip"

After AI finishes a task, ask: "What did you skip, simplify, or fake? What edges did you leave rough?" It will tell you. Fixing those is usually 20% of the effort for 50% of the quality.

## Patterns to avoid

### Persona prompts

Do not start prompts with "You are a senior architect." It is theatre. It does not make the AI a senior architect. If you want senior-architect-quality output, give it senior-architect-quality context (a reviewed architecture doc, explicit constraints, a clear story) and ask a clear question.

The exception: a brief, specific role cue can be useful for a single-turn task ("act as a code reviewer focused on security and flag anything suspicious"). The anti-pattern is building your whole workflow around maintained personas with invented names.

### "Just build it" prompts on ambiguous work

If the AI has to guess the design, it will guess confidently and wrongly. If you find yourself tempted to prompt "just build the whole feature," stop. You are missing a spec. Write the spec.

### AI as reviewer of record

AI can draft a review. It can spot issues. It cannot approve a PR, because approval carries accountability. The human who approves is the human who owns the consequences.

### Letting AI invent requirements

If the AI proposes an acceptance criterion that was not in the story, either add it to the story (with review) or reject it. Do not let requirements appear in code that never appeared in docs. Requirements that are not reviewed are not requirements, they are guesses.

### One giant conversation

Context windows are finite and even within the limit, quality degrades in very long sessions. Start fresh sessions for unrelated work. The artifacts in the repo are the continuity; the chat history is not.

## What AI is genuinely great at

- **Drafting.** First drafts of any artifact. Faster and usually no worse than a human first draft.
- **Expanding.** Bullet points into prose, terse notes into structured docs.
- **Translating.** Between formats, between languages, between abstraction levels.
- **Searching.** Finding code, finding related artifacts, finding inconsistencies.
- **Testing.** Writing tests against a clear interface.
- **Implementing well-specified work.** When the story is tight, the AI is excellent.

## What AI is genuinely poor at

- **Deciding what to build.** That is a stakeholder and product question.
- **Noticing what is missing.** It does not know what it does not know.
- **Weighing tradeoffs that involve context outside the repo.** Budget, politics, customer relationships.
- **Owning anything.** Accountability cannot be prompted into it.

## A simple check

Before you hand AI a task, ask: "If a smart new hire walked into this repo today with no prior context, would they be able to do this task from the artifacts alone?"

- If yes, AI will do well.
- If no, write more context first. Then AI will do well.

That is the whole trick.
