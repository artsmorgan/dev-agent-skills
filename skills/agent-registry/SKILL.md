---
name: agent-registry
description: Bootstrap an AGENTS.md that routes a request to the right specialist agent, keeps one agent owning each deliverable, and separates agent methodology from client/project facts. Use when a project needs more than one specialist agent (copywriter, SEO, brand, sales, etc.) and requests currently get handled ad hoc, when asked to "set up agent routing", "define our agents", or when a new specialization becomes repeatedly useful and needs its own instruction file.
---

# Agent Registry

A template for a project's `AGENTS.md` — the canonical registry of which specialist
agent handles which kind of request, how multi-agent work hands off, and how
conflicts between instructions get resolved.

This is a **pattern**, not a fixed roster. The example in
[`AGENTS.md.template`](AGENTS.md.template) is populated with content-agency
agents (`COPYWRITER`, `SEO`, `RESEARCH`, `BRAND_STRATEGIST`, `SALES_STRATEGIST`,
`CONTENT_STRATEGIST`) — swap the roster for whatever specialists your project
actually needs (e.g. `FRONTEND`, `BACKEND`, `DATA`, `SECURITY`).

## When to use this

- More than one recognizable discipline touches the work, and routing between
  them is currently done informally.
- You keep re-explaining the same specialist's scope and boundaries.
- You want one agent to own final coherence per deliverable, even when others
  contributed strategy or review.

## Do

1. Copy `AGENTS.md.template` to the project root as `AGENTS.md` and rename it
   to fit — replace the example roster with your project's actual agents.
2. For each agent listed, create its own `<AGENT_NAME>_AGENT.md` instruction
   file (capabilities and methodology only).
3. Keep project/client-specific facts (positioning, voice, prior decisions) in
   separate files — never inside an agent's instruction file. See section 8 of
   the template for the recommended split.
4. Add new agents only when a specialization becomes *repeatedly* useful —
   don't pre-create agents you don't need yet.

## Do not

- Simulate a multi-agent workflow when the task fits in one discipline.
- Mix "how this agent works" with "what is true about this client/project" in
  the same file.
- Let a later instruction silently overwrite an already-established fact
  (positioning, terminology, prior decision) without flagging the change.

## DONE when

`AGENTS.md` lists every active agent with a purpose and routing rule · every
listed agent has its own instruction file (or is explicitly marked as not yet
implemented) · conflict-resolution order is stated.
