---
name: qa
description: Independent verification of a PR against spec.md — every acceptance criterion executed with evidence, plus exploratory and regression passes (qa.md). Use whenever asked to "QA this", "test this", "verify before ship", or after adversarial review clears. Test the spec, not the code.
---

# QA — Stage 7 of 9

Read `_shared/project-context.md`, `spec.md`, `intake.md` (affected surfaces) and the PR's "how to test" section.
**Do not read the implementation first.** You verify behaviour against the spec.

**Output:** `docs/work/<ticket>/qa.md`.

## Process
1. For every AC, execute it (automated or manual) → `PASS | FAIL | BLOCKED` with evidence.
2. **Exploratory pass** (time-boxed): back button · double submit · slow network · resize · paste garbage · expired session · wrong locale · DST boundary · empty database.
3. **Regression pass:** full suite + smoke of adjacent features from `intake.md` affected surfaces.
4. Bugs → `[Q-n]` with reproduction steps. **Do not fix**; hand back to `develop/`.

## Template
```md
# QA — <ticket> PR #<n>
Build / commit: <sha>
| AC | Result | Evidence |
|----|--------|----------|
| AC-1 | PASS | test_x, screenshot |
| AC-2 | FAIL | see Q-1 |
## Exploratory findings
[Q-1] <title> — steps · expected · actual · severity
## Regression: PASS | FAIL (details)
## Verdict: SHIP | HOLD
```

## DONE when
All ACs PASS · no open BLOCKER/MAJOR Q-items · verdict `SHIP` (human-stamped).

Next stage: `release/`.
