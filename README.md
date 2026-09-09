# dev-agent-skills

A collection of open source skills for coding agents (Claude Code, Cursor, Codex,
Copilot, Windsurf, Aider, etc.) that I use in my own development projects.

Each skill lives in its own folder under [`skills/`](skills/) with at least one
`SKILL.md` file describing what it is, when to use it, and how. Copy the folder
you need into your own project — you don't need the whole repo.

## Available skills

| Skill | What it does |
|-------|---------------|
| [`eng-pipeline/`](skills/eng-pipeline/) | A 9-stage pipeline that takes a ticket from intake to production (intake → spec → spec-review → plan → develop → adversarial-review → qa → release → retro), each stage a standalone skill with a clear input/output. |
| [`agent-registry/`](skills/agent-registry/) | An `AGENTS.md` template for projects with more than one specialist agent: defines routing by discipline, who owns the final deliverable, and separates agent methodology from project/client facts. |

## Usage

```bash
git clone https://github.com/artsmorgan/dev-agent-skills.git
cp -r dev-agent-skills/skills/<skill-name> your-project/.claude/skills/
```

### By tool

**Claude Code** — copy the folders into `.claude/skills/`. Invoke with
`/<name>` (e.g. `/intake`, `/spec`).

**Cursor** — copy each `SKILL.md` into `.cursor/rules/<name>.mdc` with
`alwaysApply: false`; reference with `@<name>`.

**Codex / Copilot / Windsurf / Zed / Aider** — keep the folders anywhere in
the repo (e.g. `skills/`) and add to your `AGENTS.md`:
```
Skills live in skills/. Before starting a task, identify the stage and read
skills/<stage>/SKILL.md in full.
```

## Structure

```
skills/
  <skill-name>/
    SKILL.md          # or a multi-stage skill with sub-folders, each with its own SKILL.md
    ...
```

## License

MIT — see [LICENSE](LICENSE).
