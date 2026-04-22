# Role: Mobile Developer (Android + iOS)

You build the apps users carry in their pockets. In CAIRN, mobile is treated as a single role covering both platforms, because the CAIRN flow (spec, story, review) is the same regardless of which platform the code runs on. Platform-specific concerns live inside the stories and the architecture.

## Who you are

- You work across at least one of Android (Kotlin/Java) and iOS (Swift/Objective-C), often both.
- You think in terms of OS capabilities, form factors, and lifecycle events.
- You care about performance, battery, and permissions.
- You design for offline, bad networks, and interruptions. All the time.

## Artifacts you own

- Stories in `tasks/mobile/`. Stories can be platform-specific or cross-platform; name them clearly.
- Mobile-specific sections of `architecture.md` (navigation, state, offline behaviour, background tasks).
- Platform-specific conventions in your repo's CLAUDE.md or a dedicated mobile section.

## Artifacts you contribute to

- UX research: review for mobile interaction feasibility.
- `architecture.md`: push back when the design ignores mobile realities (battery, background limits, platform restrictions).
- Backend stories: review API shapes for mobile-friendliness (payload size, batching, auth patterns).

## Platform separation in stories

For non-trivial features, split stories per platform:

```
tasks/mobile/
  QUIZ-04-player-join-android.md
  QUIZ-05-player-join-ios.md
  QUIZ-06-player-join-shared-contracts.md
```

For simple features, or when you have a shared codebase (Flutter, React Native, Kotlin Multiplatform), a single `tasks/mobile/` story is fine. Be honest about what is shared and what is not.

## How AI fits your work

- **Platform-specific boilerplate.** AI does well at common patterns: networking, navigation, local storage, background work, permissions.
- **Cross-platform translation.** Given a working iOS implementation, AI can produce a first-pass Android translation. You verify.
- **Lifecycle handling.** Handy for reminding you which lifecycle events you need to handle.
- **Platform idioms.** Ask AI to review your code against platform idioms (e.g. "does this feel Swift-idiomatic?"). Useful as a second opinion.
- **Accessibility checks.** Both platforms have strong accessibility APIs; AI is a good starter-checker.

## How AI does not help

- It does not run on a device. Emulators are not the same as real phones.
- It does not know your team's chosen patterns for DI, navigation, or state. Feed them via CLAUDE.md.
- It will mix platform APIs. Verify every call.
- It underestimates how much real-world behaviour depends on OS version quirks.
- Its knowledge of the latest SDK is often stale. Verify APIs.

## Anti-patterns for this role

- **Testing only on the emulator.** Real devices behave differently. Use them for at least one pass before merging.
- **Ignoring offline and bad-network cases.** Mobile users spend a lot of time with no signal. Design and code for it.
- **Copying cross-platform without reviewing idioms.** Swift-flavoured Kotlin is painful to maintain. Translate thoughtfully.
- **Merging without checking both platforms.** If your story covers both, both are part of "done."
- **Over-engineering abstraction layers.** AI and enthusiastic devs both love abstractions. Most mobile features do not need them.

## A day in the life (iOS example)

**09:00.** Read the story, the linked UX flow, and the API contract.

**09:30.** Branch. AI session primed with the story, `CLAUDE.md`, and the iOS architecture notes. Ask for the plan.

**10:00.** Implement the view, view-model, and networking. Handle error and loading states. Add offline cache.

**13:00.** Test on simulator. Works. Test on your real device. Notice it breaks when you tether via a flaky network. Add retry.

**14:30.** Write UI tests for the happy path and one failure case.

**16:00.** Open Code PR. Attach a short screen recording.

**17:00.** Review from Android dev ensures the contract is shared correctly. Merged.

## The hidden job

Your hidden job is to protect the product from the assumption that "mobile is just web on a smaller screen." It is not. Battery, permissions, lifecycle, offline, and platform conventions are first-order concerns. If the design ignores them, you are the one who raises the flag early. Better to raise it in the Spec PR than at the end of implementation.
