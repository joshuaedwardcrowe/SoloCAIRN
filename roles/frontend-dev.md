# Role: Frontend Developer

You build what users actually see and touch on the web. In ACAIRN, you own the frontend stories end to end and translate UX intent into working interfaces.

## Who you are

- You think about interaction, state, and feel.
- You care about performance, accessibility, and browser quirks.
- You implement the UX designer's intent, but you push back when the design misses a technical constraint.
- You know that the frontend is where most user-facing bugs live.

## Artifacts you own

- Your assigned stories in `features/<feature>/stories/frontend/`.
- Frontend-specific sections of `architecture.md` (state management, data fetching patterns, component structure).
- Shared component and design system contributions, if your team has them.

## Artifacts you contribute to

- UX research: you review for implementation feasibility.
- `architecture.md`: you push back when the design ignores frontend realities (bundle size, runtime cost, client state complexity).
- Backend stories: you review API contracts that your frontend will consume.
- Code reviews: always on frontend PRs, sometimes cross-platform.

## How AI fits your work

- **Component drafting.** Given a wireframe and the story, AI can draft a component shell fast. You fill in the interaction details.
- **Boilerplate for well-known patterns.** Forms, lists, modals: AI does these well in a familiar stack.
- **Accessibility review.** Ask AI to review a component for ARIA correctness, keyboard navigation, focus management. Good starter checklist.
- **Test generation.** Unit tests and component tests against the acceptance criteria.
- **Visual regression explanations.** When a test fails on a visual diff, AI can usually explain what changed.

## How AI does not help

- It does not know your design system without being told.
- It will confidently invent props and components that do not exist in your codebase.
- Its default styling is generic. Without your patterns in context, output feels off-brand.
- It does not feel the UI. You still have to run it and interact with it.

## Anti-patterns for this role

- **Shipping without actually interacting with the UI.** Running tests is not the same as using the feature. Open the browser.
- **Copy-pasting AI components without verifying imports.** Half of AI-generated components include plausible-but-nonexistent imports.
- **Ignoring the edge states.** Loading, empty, error, offline. The design usually covers these. Implement them.
- **Letting AI invent copy.** Microcopy is a design decision. Use what UX provided, or escalate.
- **Over-engineering state.** AI loves to introduce state management libraries. Push back unless genuinely needed.

## A day in the life

**09:00.** Review your story, the linked UX wireframes, and the API contract for the endpoints you will hit.

**09:30.** Branch in the code repo. Start an AI session with both the code repo and the ACAIRN repo open in the IDE workspace. "Implement `features/pub-quiz/stories/frontend/QUIZ-03-host-console.md` from the ACAIRN repo. Follow the components in our design system (see `src/components/` in the code repo). Show me the plan first."

**10:00.** Implement the main component, with states for loading, empty, success, error. Wire up API calls.

**12:00.** Open the feature in the browser. Interact with it. Notice a missing focus ring on the primary button. Fix.

**13:00.** Write tests for the main flow and the error state.

**15:00.** Open a draft Code PR. Take screenshots of the primary states and attach to the PR.

**16:00.** Address UX review (they want tighter spacing on the score column). Fix.

**17:00.** Address a code review (an unused import and a typo in a test). Fix. Merged.

## The hidden job

Your hidden job is to protect the user experience during implementation. The design is an intent; the frontend is the reality. A thousand small decisions you make (micro-animations, focus management, error copy) decide whether the feature feels right. Those decisions are yours. Make them on purpose.
