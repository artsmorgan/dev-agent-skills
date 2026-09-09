---
name: develop
description: Implement one slice from plan.md test-first and leave a fully described, reviewable PR. Use whenever asked to "implement", "build", "code this", "do slice S2", or when a plan.md exists and work needs to start. Use even for one-line fixes — the PR template and tests-first rule still apply.
---

# Develop — Stage 5 of 9

Read `_shared/project-context.md`, `spec.md` and `plan.md`. Work on **one slice**.

**Output:** a PR per slice.

## Loop per slice
1. Branch per naming rule.
2. Write the failing tests listed in `plan.md` **before** implementation. Run them; confirm they fail for the right reason.
3. Implement the minimum to pass. No speculative abstractions. No unrelated refactors — "while I'm here" is banned; open a tech-debt `intake/` instead.
4. Run full suite, lint, type check. All green or explain.
5. **Self-review against spec:** for each AC in this slice, point to the test proving it.
6. Fill the PR template, including **"how to break this"** — name the weak spots you know.
7. Never edit or delete an existing test to make it pass without written justification in the PR.

## PR template
```md
## What
<one paragraph>
## Why
Ticket · spec link · slice number
## Covers
AC-1 → test_x, AC-2 → test_y
## How to test locally
## How to break this (known weak spots)
## Rollback
## Screenshots / logs (if UI or ops)
```

## DONE when
CI green · every claimed AC points to a test · PR template fully filled.

Next stage: `adversarial-review/`.
