# Story: QUIZ-08 Database Schema

## Context

New tables for the quiz feature. This story lands the schema first so all other stories can build against it.

See [04-architecture.md](../../04-architecture.md) §Data.

## Acceptance criteria

- [ ] Migration adds the following tables with appropriate indexes:
  - `quiz_questions`
  - `quiz_templates`
  - `quiz_template_questions` (join table, ordered)
  - `quiz_sessions`
  - `quiz_teams`
  - `quiz_answers`
  - `quiz_scores`
- [ ] Foreign keys and cascade rules defined and reviewed.
- [ ] Indexes on hot paths: `quiz_answers(session_id, team_id, question_id)`, `quiz_sessions(code)`, `quiz_teams(session_id)`.
- [ ] Retention: `quiz_sessions` and their children purged 30 days after `ended_at`.
- [ ] Down-migration drops the tables cleanly (tested).
- [ ] Schema diagram added to `docs/features/pub-quiz/schema.md`.

## Proposed schema (sketch)

```
quiz_questions
  id (uuid, pk)
  category (text)
  difficulty (smallint)
  prompt (text)
  options (jsonb)           -- list of strings for multiple choice
  correct_answer (text)     -- for free-text; index into options for MC
  created_at, updated_at

quiz_templates
  id (uuid, pk)
  title (text)
  created_by (user_id)
  created_at

quiz_template_questions
  template_id (fk)
  question_id (fk)
  position (int)
  primary key (template_id, position)

quiz_sessions
  id (uuid, pk)
  code (text unique, 6 chars)
  template_id (fk)
  host_id (user_id)
  state (enum: pending, running, paused, ended)
  current_question_index (int)
  started_at, ended_at

quiz_teams
  id (uuid, pk)
  session_id (fk)
  name (text)
  token_hash (text)
  is_paper (bool)
  created_at

quiz_answers
  id (uuid, pk)
  session_id (fk)
  team_id (fk)
  question_id (fk)
  submitted_answer (text)
  is_correct (bool)
  points_awarded (int)
  submitted_at (timestamp)
  unique (session_id, team_id, question_id)

quiz_scores
  session_id (fk)
  team_id (fk)
  total_points (int)
  updated_at
  primary key (session_id, team_id)
```

## Files likely touched

- `database/migrations/NNNN-add-quiz-tables.sql` (new)
- `database/migrations/NNNN-add-quiz-tables.down.sql` (new)
- `docs/features/pub-quiz/schema.md` (new)

## Dependencies

- None. This story is the base dependency for the rest.

## Out of scope

- Seed data (handled in QUIZ-03).
- Data access layer (handled in each backend story).

## Notes

- `quiz_answers.unique` constraint enforces the "one submission per team per question" rule at the DB level. Backend can still reject earlier, but the constraint is the last line of defence.
- Question bank is designed to be additive: new questions append, never update.
- 30-day retention: handled by an existing scheduled job pattern. Add the quiz tables to the retention config.
