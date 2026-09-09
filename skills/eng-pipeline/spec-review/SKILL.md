---
name: spec-review
description: Adversarial review of a spec.md before any code is written — find ambiguity, untestable criteria, missing failure paths, contract breaks and hidden scope. Use whenever a spec is in draft, when asked to "review the spec", "poke holes in this", "is this spec ready", or before running plan/develop. This is the cheapest review in the pipeline; never skip it.
---

# Spec Review — Stage 3 of 9

Read `_shared/project-context.md` and `docs/work/<ticket>/spec.md`.

**Stance:** you will be blamed when this ships broken. Be harsh, be specific.
**Output:** gaps list + revised `spec.md` with status `reviewed`.

## Check, in order
1. **Ambiguity** — any sentence with two readings. Quote it, give both readings.
2. **Untestable ACs** — any AC you could not write an automated or manual test for.
3. **Missing paths** — for every state-changing operation: runs twice? fails halfway? runs concurrently? no data? wrong user?
4. **Contract breaks** — public API, event shape or DB column others depend on. `grep` for consumers and list them.
5. **Silent scope** — requirements implying unlisted work (new field ⇒ migration + validation + serializer + UI + tests).
6. **Non-goal collisions** — any AC contradicting a non-goal.

## Output format
```md
[G-1] BLOCKER | MAJOR | MINOR
Where: <section / AC-n>
Issue: <one sentence>
Proposed rewording: <exact text>
```
BLOCKER = cannot be implemented as written · MAJOR = will cause rework · MINOR = clarity.

Apply accepted rewordings to `spec.md`, set `Status: reviewed`. A human sets `approved`.

## Do not
Approve with zero findings unless you list what you checked and why it held.

## DONE when
Zero BLOCKERs · all MAJORs fixed or accepted in writing by a human · status `approved`.

Next stage: `plan/`.
