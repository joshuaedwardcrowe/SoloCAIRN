# Role: Contributor

You pick up a story and build it. That's it — you might be the Maintainer switching hats, or you might be an intermittent outside contributor who's never touched this codebase before and is picking up a single issue. Either way, the story (or GitHub Issue) has everything you need to start.

## Who you are

- You own the Build stage for whatever you picked up — nothing upstream of it, nothing downstream.
- You think in terms of the story's acceptance criteria, not the whole feature.
- You read before you write: the story, and whatever architecture/scope context it links to.

## Artifacts you own

- Your Code PR — the implementation of exactly one story/issue. Draw on whichever skill matches the work: [Backend Development](../skills/backend-dev.md), [Frontend Development](../skills/frontend-dev.md), or [Mobile Development](../skills/mobile-dev.md).

## Artifacts you contribute to

- The story itself, if Build reveals it was wrong or missing something — see [Revising mid-flight](../docs/03-lifecycle.md#revising-mid-flight). Flag it, don't silently route around it.

## How AI fits your work

- **Plan-first implementation.** Point AI at the story (and the architecture doc, if one exists) and ask for a plan before it writes anything. Review the plan, then implement.
- **Test generation.** Given a story's acceptance criteria, AI drafts a solid first pass of tests. You review, tighten, and add what it missed.
- **Code archaeology.** "Where does this codebase currently handle X" is fast to answer in a well-structured repo.

## How AI does not help

- It does not know this codebase's quirks without being told. Feed it context, or its suggestions will be generic.
- It invents libraries and APIs. Check every import.
- It will produce something plausible-looking even when it's wrong — reading the diff is still your job, not optional.

## Anti-patterns for this role

- **Shipping AI-drafted code without reading it.** If you didn't read it, you don't know what you shipped.
- **Silently routing around a wrong story.** If implementation reveals the design is wrong, say so — update the artifact, don't quietly "fix" it in code and hope nobody notices the drift.
- **One giant PR.** If your change has more than a few hundred lines of meaningful diff, the story was probably too big — see [PR size limits](../CONTRIBUTING.md) wherever this repo sets one.

## On review, honestly

CAIRN's "review is the stage gate" (Manifesto principle 3) assumes an independent second reviewer. SoloCAIRN often doesn't have one. Two real cases:

- **A Contributor is available who isn't you.** Normal review happens — a genuine second pair of eyes, exactly as CAIRN intends.
- **It's genuinely just you.** Review becomes self-review, and it only works if you make it structurally different from writing: step away and come back with a real gap (hours, not minutes), per [principle 10, the producer verifies first](../MANIFESTO.md). Checking your own work in the same sitting you wrote it isn't review, it's a rubber stamp — name that honestly rather than pretend the gate is doing something it isn't.

## The hidden job

Your hidden job — whether you're the Maintainer or a first-time outside contributor — is to notice when the story doesn't match reality, and say so, rather than quietly building around the gap. The story file is the record everyone else (including future-you) relies on; letting it drift silently is worse than admitting it was wrong.
