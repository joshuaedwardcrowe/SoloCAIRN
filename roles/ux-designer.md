# Role: UX Designer / Researcher

You are the person who watches users, designs flows, and makes sure the interface matches the intent. In CAIRN, your artifacts shape both what gets built and how it feels.

## Who you are

- You understand users through observation, not assumption.
- You think in flows, not screens.
- You care about the edges: errors, empty states, edge cases.
- You can sketch fast and prototype faster.

## Artifacts you own

- `ux-research.md`: themes and opportunities from research.
- Wireframes, flows, prototypes: lived under `features/<feature>/ux/` in the CAIRN repo.
- Persona docs and journey maps, when relevant.
- Design system contributions: patterns that should be reused.

## Artifacts you contribute to

- `problem-statement.md`: you review for alignment with what you have seen in research.
- `scope.md`: you push back on scope that ignores UX consequences.
- Stories: you add acceptance criteria about states, transitions, and edges.
- Code PRs: you review the rendered output, not the code.

## How AI fits your work

- **Research synthesis.** Feed interview notes; get clustered themes. You validate.
- **Competitor landscape scans.** Ask AI to summarise how five competitors solve a similar flow. You cross-check the claims (AI can invent features that do not exist).
- **Prototype copy.** First draft of button labels, empty-state text, error messages.
- **Accessibility checks.** Ask AI to review a flow description for accessibility gaps. Treat as a starter checklist, not gospel.
- **Journey map drafts.** From bullet observations, draft a journey map structure. You fill the detail.

## How AI does not help

- It does not watch users. Research is still a human activity.
- It does not know your design system without being told. If you want consistent patterns, feed it the patterns.
- Its default design choices are generic and often bad for your specific audience.
- It hallucinates features in competitor scans. Verify before citing.

## Anti-patterns for this role

- **Wireframing without research.** Beautiful wireframes for the wrong problem waste everyone's time.
- **Research docs nobody reads.** If your research is 20 pages, write a one-page summary. The summary is the artifact that gets used.
- **Handing off pixels without intent.** A screenshot without a written intent ("why is this here, what should happen when X") will be implemented wrongly. Add the intent.
- **Skipping the edges.** Happy-path flows that ignore errors and empty states will produce happy-path implementations that break in production.

## A day in the life

**Morning.** Review interview notes from the BA. Extract three candidate themes. Sketch a rough journey map on paper.

**Late morning.** Turn the sketch into a proper flow diagram. Save under `features/<feature>/ux/journey.svg` in the CAIRN repo. Write a short `ux-research.md` that explains what the diagram shows and what it implies for the design.

**Afternoon.** Start on wireframes for the two key screens. Export as PNGs to the repo. Update `ux-research.md` with links.

**Late afternoon.** Review the story drafts. Add acceptance criteria for error states, empty states, loading states. Comment on any story where the design is ambiguous.

## The hidden job

Your hidden job is to keep the team's attention on the user, not the feature. It is easy for a team deep in implementation to optimise for their own ease. You are the counterweight. Your artifacts are the record of what the user actually needs.
