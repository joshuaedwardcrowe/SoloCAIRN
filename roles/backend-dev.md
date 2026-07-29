# Role: Backend Developer

You build the services, the APIs, the data flows. In SoloCAIRN, you own the backend stories end to end, and you contribute to architecture decisions as a specialist.

## Who you are

- You think in terms of systems, data, and failure modes.
- You care about correctness, performance, and the cost of complexity.
- You understand your stack deeply and borrow from others carefully.
- You write tests because you have been burned by not writing tests.

## Artifacts you own

- Your assigned stories in `features/<feature>/stories/backend/`.
- Backend-specific sections of `architecture.md`.
- Feature-scoped data model notes, if you are the database-facing dev on the team.
- Backend runbooks for services you own (project-level, not SoloCAIRN).

## Artifacts you contribute to

- `architecture.md`: you push back on designs that misunderstand the backend.
- Stories for other platforms: you review stories that depend on backend work.
- Code reviews: for backend PRs, always; for others, when asked.

## How AI fits your work

- **Plan-first implementation.** Start an AI session. Point it at the story and the architecture. Ask for a plan. Review the plan. Then implement.
- **Test generation.** Given a story's acceptance criteria, AI is excellent at writing a first pass of tests. You review, tighten, and add edges it missed.
- **Code archaeology.** "Where do we currently handle retries for outbound HTTP calls?" is the sort of question AI answers fast in a well-structured repo.
- **Refactoring drafts.** AI is good at mechanical refactors. Always review the diff carefully.
- **Migration drafts.** AI can produce a first-pass migration script. You treat it as a proposal, never as final.

## How AI does not help

- It does not know your production data shapes without being told.
- Its default error handling is either too paranoid or too lax, rarely right.
- It invents libraries. Check every import.
- It does not know your system's performance characteristics. If an approach requires a load test, it still requires a load test.

## Anti-patterns for this role

- **Shipping AI-drafted code without reading it.** If you did not read it, you do not know what you shipped.
- **Hand-waving tests.** "Tests pass" is not the same as "the feature works under load, at the edges, across restarts."
- **Ignoring the story's acceptance criteria.** If the story says "retry up to 3 times," and your code retries forever, the story is not done.
- **Silent scope growth.** If implementation reveals that the design is wrong, stop and update the design with a comment, do not silently "fix" it in code.
- **One giant PR.** If your code PR has more than a few hundred lines of meaningful change, your story was probably too big.

## A day in the life

**09:00.** Check the SoloCAIRN repo for today's story. Read it carefully.

**09:15.** Branch off main in the code repo. Start an AI session with both the code repo and the SoloCAIRN repo open in the IDE workspace. Prompt: "Implement `features/pub-quiz/stories/backend/QUIZ-01-session-service.md` from the SoloCAIRN repo. Show me the plan first, respecting our project conventions and the architecture at `features/pub-quiz/architecture.md`."

**09:30.** Review the plan. Push back on one aspect (the caching strategy does not fit this use case). AI re-plans.

**10:00.** Implement. Iterate. Run tests locally. Fix what breaks.

**13:00.** Acceptance criteria all met. Open a draft Code PR so teammates can see progress.

**14:30.** Address first review comments.

**16:00.** Mark PR ready. Request review.

**17:00.** Merged. Move to the next story.

## The hidden job

Your hidden job is to notice when the architecture is becoming wrong. Implementation reveals what design could not. When you hit a wall, your job is to surface it, not to quietly route around it. The story file, the architecture doc, and the team deserve to know. That noticing is what makes you a senior backend dev, not the code you ship.
