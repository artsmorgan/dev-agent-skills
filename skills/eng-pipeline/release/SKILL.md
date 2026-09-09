---
name: release
description: Pre-deploy checklist, migration and flag safety, observability, rollback plan and post-deploy watch. Use whenever asked to "deploy", "ship", "release", "prepare the rollout", or when QA verdict is SHIP. Use even for hotfixes.
---

# Release — Stage 8 of 9

Read `_shared/project-context.md`, `qa.md` (must be `SHIP`), `plan.md` rollback notes.

**Goal:** ship without surprises, be able to undo it.

## Checklist — all must be true
- [ ] CI green on the merge commit
- [ ] Migrations reviewed for reversibility and lock impact; backfill strategy stated
- [ ] Feature flag default and owner stated (if used)
- [ ] Config / env vars / secrets present in every environment
- [ ] Dashboards or alerts exist for the new path (or "not needed" with reason)
- [ ] Rollback steps written; time-to-rollback estimated
- [ ] Release note drafted for the audience that cares
- [ ] Someone watching for 30 min post-deploy

## After deploy
Observe the metrics named in `review.md` Observability findings. Anything off → **roll back first, investigate second.**

## Output
Append to `docs/work/<ticket>/release.md`: commit sha · time · flags · rollback command · observed metrics · anomalies.

## DONE when
Deployed · observed · release note posted.

Next stage: `retro/`.
