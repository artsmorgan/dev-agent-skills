---
name: spec
description: Write a spec-first document (spec.md) with numbered Given/When/Then acceptance criteria, data/contract changes and explicit non-goals from an intake.md. Use whenever asked to "write the spec", "define requirements", "what should this do", or before any implementation starts. Use even for small changes — small specs are fine, missing specs are not.
---

# Spec — Stage 2 of 9

Read `_shared/project-context.md` and `docs/work/<ticket>/intake.md` first. If no intake exists, run `intake/` first.

**Goal:** a document a stranger could implement and a tester could verify without talking to you.
**Output:** `docs/work/<ticket>/spec.md`, status `draft`.

## Rules
- Every requirement has ≥1 acceptance criterion (AC) in Given/When/Then form, numbered `AC-n`.
- Every AC is **observable**: a test, log line, UI state, or API response. Reject "works well", "is fast" → write "p95 < 300 ms on endpoint X".
- Cover: happy path · each failure mode · empty/null/boundary inputs · permissions · concurrency (if shared state) · timezone/i18n (if dates or money).
- Name every data change (migrations, fields) and API/event contract change explicitly.
- List **non-goals**. A spec without non-goals is not done.
- Edge cases and failure modes get their own AC numbers.

## Template
```md
# Spec — <ticket> <title>
Status: draft | reviewed | approved
Links: intake.md, design, related tickets

## Goal
## Non-goals
## User-facing behaviour
## Data & contracts
- Migrations: …
- API changes: …
- Events / jobs: …

## Acceptance criteria
AC-1  Given … When … Then …
AC-2  …

## Constraints
performance / security / compliance / feature flag

## Risks & unknowns
```

## DONE when
Every requirement maps to an AC · every AC testable · non-goals listed · status `draft`.

Next stage: `spec-review/`.
