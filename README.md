# dev-agent-skills

Colección de skills open source para Claude Code que uso en mis proyectos de desarrollo.

## ¿Qué es esto?

Cada skill vive en su propia carpeta bajo [`skills/`](skills/) con un archivo `SKILL.md` que describe cuándo y cómo se usa. Podés copiar la carpeta de la skill que te interese a tu propio proyecto (`.claude/skills/`) o instalarla como parte de un plugin.

## Uso

```bash
git clone https://github.com/artsmorgan/dev-agent-skills.git
cp -r dev-agent-skills/skills/<nombre-skill> tu-proyecto/.claude/skills/
```

## Estructura

```
skills/
  <nombre-skill>/
    SKILL.md
    ...
```

## Licencia

MIT — ver [LICENSE](LICENSE).
