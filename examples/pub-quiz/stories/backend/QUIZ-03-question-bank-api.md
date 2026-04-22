# Story: QUIZ-03 Question Bank API

## Context

The host needs to build a quiz from our pre-built question bank. This story exposes the bank and supports quiz template creation.

See [04-architecture.md](../../04-architecture.md) §Components.

## Acceptance criteria

- [ ] `GET /questions` returns paginated questions with filters: `category`, `difficulty`, `search`.
- [ ] `GET /questions/{id}` returns a single question with answers.
- [ ] `POST /quiz-templates` accepts a list of question IDs and a title, returns a template ID.
- [ ] `GET /quiz-templates/{id}` returns the stored template with resolved question content.
- [ ] Question answers are not returned in any endpoint accessible to player clients. Only host and server components access the answer field.
- [ ] Seed data: 500 questions imported across 10 categories from `api/seeds/quiz-questions.json`.

## Files likely touched

- `api/src/routes/quiz-questions.ts` (new)
- `api/src/routes/quiz-templates.ts` (new)
- `api/src/services/quiz-question-bank.ts` (new)
- `api/seeds/quiz-questions.json` (new)
- `api/src/migrations/NNNN-seed-quiz-questions.ts` (new)

## Dependencies

- Depends on: [QUIZ-08](../database/QUIZ-08-schema.md)

## Out of scope

- Host-authored questions (deferred to v2).
- Question editing UI (covered indirectly in QUIZ-04).
- Content moderation tools.

## Notes

- Answer field protection: add a route-level check. Covered by a test that asserts the player token cannot fetch answers.
- Seed data source: the BA is assembling a CSV. Converted to JSON during import.
