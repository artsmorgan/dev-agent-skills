# dev-agent-skills

Colección de skills open source para agentes de código (Claude Code, Cursor, Codex,
Copilot, Windsurf, Aider, etc.) que uso en mis proyectos de desarrollo.

Cada skill vive en su propia carpeta bajo [`skills/`](skills/) con al menos un
archivo `SKILL.md` que describe qué es, cuándo usarla y cómo. Copiá la carpeta
que te interese a tu propio proyecto — no hace falta el repo entero.

## Skills disponibles

| Skill | Qué hace |
|-------|----------|
| [`eng-pipeline/`](skills/eng-pipeline/) | Pipeline de 9 etapas para llevar un ticket de intake a producción (intake → spec → spec-review → plan → develop → adversarial-review → qa → release → retro), cada etapa como skill independiente con input/output claro. |
| [`agent-registry/`](skills/agent-registry/) | Template de `AGENTS.md` para proyectos con más de un agente especialista: define ruteo por disciplina, quién es dueño del entregable final, y separa metodología de agente vs. hechos del proyecto/cliente. |

## Uso

```bash
git clone https://github.com/artsmorgan/dev-agent-skills.git
cp -r dev-agent-skills/skills/<nombre-skill> tu-proyecto/.claude/skills/
```

### Por herramienta

**Claude Code** — copiá las carpetas a `.claude/skills/`. Se invocan con
`/<nombre>` (ej. `/intake`, `/spec`).

**Cursor** — copiá cada `SKILL.md` a `.cursor/rules/<name>.mdc` con
`alwaysApply: false`; referenciá con `@<name>`.

**Codex / Copilot / Windsurf / Zed / Aider** — dejá las carpetas en el repo
(ej. `skills/`) y agregá a tu `AGENTS.md`:
```
Skills live in skills/. Before starting a task, identify the stage and read
skills/<stage>/SKILL.md in full.
```

## Estructura

```
skills/
  <nombre-skill>/
    SKILL.md          # o una skill multi-etapa con sub-carpetas, cada una con su SKILL.md
    ...
```

## Licencia

MIT — ver [LICENSE](LICENSE).
