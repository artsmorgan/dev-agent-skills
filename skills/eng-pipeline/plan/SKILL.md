---
name: plan
description: Slice an approved spec.md into small, independently mergeable PRs with tests-first lists, ordering, flags and rollback per slice (plan.md). Use whenever asked to "break this down", "plan the work", "how do we split this", or before starting development on any spec with more than one acceptance criterion.
---

# Plan — Stage 4 of 9

Read `_shared/project-context.md` and `docs/work/<ticket>/spec.md` (must be `approved`).

**Goal:** slices a reviewer can hold in their head.
**Output:** `docs/work/<ticket>/plan.md`.

## Rules
- Each slice ≤ ~400 changed lines, independently mergeable, behind a flag if it would expose incomplete behaviour.
- Order so `main` stays green and deployable after each slice.
- For each slice list the **tests to write first**, mapped to AC numbers.
- Flag what can run in parallel and what has external dependencies.
- Default order: schema → domain logic → API → UI. Deviate only with a stated reason.
- Any list endpoint gets a query-count assertion in tests-first.

## Template
```md
# Plan — <ticket>
## Slices
S1  <title> — covers AC-1, AC-2
    Files: …
    Tests first: test_x (AC-1), test_y (AC-2)
    Flag: <name> | none
    Depends on: —
    Rollback: …
S2  …
## Parallelisable: S2 ∥ S3
## External dependencies / risks
```

## DONE when
Every AC covered by ≥1 slice · every slice has tests-first and rollback.

Next stage: `develop/` (one slice at a time).
