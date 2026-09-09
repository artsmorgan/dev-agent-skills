---
name: retro
description: Close the loop after a ticket ships — trace every review/QA finding and incident to the stage that should have caught it and turn it into a one-line rule in that stage's skill. Use whenever a ticket is released, when asked "what did we learn", "retro", "post-mortem", or after any rollback. Not optional.
---

# Retro — Stage 9 of 9

Read `review.md`, `qa.md`, `release.md` and any spec-review BLOCKERs for the ticket.

**Goal:** the pipeline is better than before this ticket.

## Process
1. Collect every `G-n` BLOCKER, `R-n`, `Q-n`, rollback or incident.
2. For each: **which earlier stage should have caught this?**
3. Write a concrete, one-line rule and add it to that stage's `SKILL.md`.
4. If a stage's rules exceed ~40 lines, consolidate before adding.
5. Delete any rule not triggered in the last quarter.

## Template
```md
# Retro — <ticket>
| Finding | Found in | Should have been caught in | Rule added to |
|---------|----------|----------------------------|---------------|
| R-3 N+1 on orders | adversarial-review | plan | plan/SKILL.md: "query-count assertion for list endpoints" |
## Process friction (what slowed us down)
## Keep doing
```

## DONE when
Every finding has a root stage · skill files updated (or "no change" justified) · `retro.md` committed.
