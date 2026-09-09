---
name: adversarial-review
description: Attack a PR assuming it is wrong — correctness, security, data integrity, failure handling, performance, observability, test quality — and produce severity-tagged findings (review.md). Use whenever asked to "review this PR", "code review", "find bugs", "is this safe to merge", or when any PR is opened. Never approve without listing what was tried.
---

# Adversarial Review — Stage 6 of 9

Read `_shared/project-context.md`, `spec.md`, `plan.md`, **then** the diff. Never the diff alone.

**Stance:** find the reason this pages someone at 3 a.m. You are not here to approve.
**Output:** `docs/work/<ticket>/review.md`.

## Process
1. **Run the code.** Reviews that execute nothing are opinions.
2. Attack in order, one finding per hit:
   - **Correctness** — does each AC actually hold? Try inputs the tests don't.
   - **Security** — injection, authZ bypass, IDOR, mass assignment, secrets, unsafe deserialisation, SSRF, missing rate limits.
   - **Data integrity** — transactions, idempotency, races, partial failure, migration reversibility, backfill on existing rows.
   - **Failure handling** — third party down? DB timeout? Errors swallowed? What does the user see?
   - **Performance** — N+1, unbounded queries, missing indexes for new query patterns, work inside loops.
   - **Observability** — can you tell from logs/metrics this is working or failing in prod?
   - **Maintainability** — naming, dead code, duplication, comments that lie.
3. Verify each item in the PR's own "how to break this" is mitigated or consciously accepted.
4. Judge test **quality**: do they assert behaviour or implementation? Would they catch a regression?

## Finding format
```md
[R-1] BLOCKER | MAJOR | MINOR | NIT
Where: path/file.ext:L120
What: <one sentence>
Proof: <input / steps / snippet>
Fix: <concrete suggestion>
```
BLOCKER = cannot merge · MAJOR = fix before release · MINOR = fix or ticket · NIT = optional.

## Do not
Rewrite the author's code wholesale · bikeshed what the linter enforces · "LGTM" with no findings unless you list what you tried and why it held.

## DONE when
Zero BLOCKERs · MAJORs fixed or accepted in writing · `review.md` committed.

Next stage: `qa/`.
