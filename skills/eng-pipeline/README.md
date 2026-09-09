# Engineering Pipeline Skills

Nine standalone skills. Each one is a folder with a single `SKILL.md`. Load only the one for the stage you are in.

| Stage | Skill | Input → Output |
|-------|-------|----------------|
| 1 | `intake/` | issue / message → `intake.md` |
| 2 | `spec/` | `intake.md` → `spec.md` |
| 3 | `spec-review/` | `spec.md` → gaps list + revised `spec.md` |
| 4 | `plan/` | approved `spec.md` → `plan.md` |
| 5 | `develop/` | `plan.md` → PRs (one per slice) |
| 6 | `adversarial-review/` | PR → `review.md` |
| 7 | `qa/` | PR + `spec.md` → `qa.md` |
| 8 | `release/` | green QA → deploy + rollback note |
| 9 | `retro/` | all artifacts → `retro.md` + skill edits |

`_shared/project-context.md` is filled once per repo and referenced by every skill. Artifacts live in `docs/work/<ticket>/`.

## Install

**Claude Code** — copy folders into `.claude/skills/`. Invoke with `/intake`, `/spec`, etc.

**Cursor** — copy each `SKILL.md` into `.cursor/rules/<name>.mdc` with `alwaysApply: false`; reference with `@<name>`.

**Codex / Copilot / Windsurf / Zed / Aider** — keep the folders anywhere in the repo (e.g. `skills/`) and add to `AGENTS.md`:
```
Skills live in skills/. Before starting a task, identify the stage and read skills/<stage>/SKILL.md in full. Always read skills/_shared/project-context.md.
```

## Rules that apply to every skill
- No stage starts until the previous stage's DONE criteria are met. Skipping requires a stated reason and human confirmation.
- Read before writing. Evidence over assertion. Tag uncertainty inline: `[ASSUMED]` `[UNVERIFIED]` `[NEEDS HUMAN]`.
- Anything outside the spec becomes a new Intake, never a commit.
- Max 3 clarifying questions per stage; otherwise proceed with tagged assumptions.
- Finish every stage with a 4-line report: what you did · what is DONE · what remains · what needs a human decision.
