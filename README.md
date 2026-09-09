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

### `eng-pipeline/` — what each stage does

| # | Stage | Does | Input → Output |
|---|-------|------|-----------------|
| 1 | `intake/` | Turns a vague issue, bug report or Slack message into a bounded problem statement. No solutions, no estimates — just what's known, what's assumed, and what's explicitly out of scope. | issue/message → `intake.md` |
| 2 | `spec/` | Writes a spec a stranger could implement and a tester could verify, with numbered Given/When/Then acceptance criteria, data/contract changes and non-goals. | `intake.md` → `spec.md` (draft) |
| 3 | `spec-review/` | Adversarially reviews the spec before any code exists: ambiguity, untestable criteria, missing failure paths, contract breaks, silent scope. | `spec.md` → severity-tagged gaps + revised `spec.md` (reviewed) |
| 4 | `plan/` | Slices an approved spec into small, independently mergeable PRs, ordered so `main` stays deployable, with tests-first per slice. | `spec.md` (approved) → `plan.md` |
| 5 | `develop/` | Implements one slice test-first and leaves a fully described, reviewable PR — no unrelated refactors, no speculative abstractions. | `plan.md` slice → PR |
| 6 | `adversarial-review/` | Attacks a PR assuming it's wrong: correctness, security, data integrity, failure handling, performance, observability, test quality. | PR → `review.md` |
| 7 | `qa/` | Independently verifies the PR against the spec (not the implementation) — every AC executed with evidence, plus exploratory and regression passes. | PR + `spec.md` → `qa.md` |
| 8 | `release/` | Runs the pre-deploy checklist (migrations, flags, rollback plan, observability), ships, and watches post-deploy. | green QA → deploy + rollback note |
| 9 | `retro/` | Traces every finding/incident back to the stage that should have caught it and turns it into a one-line rule added to that stage's `SKILL.md`. | all artifacts → `retro.md` + skill edits |

<details>
<summary>Sample: <code>intake.md</code> output (stage 1)</summary>

```md
# Intake — ACME-482 Duplicate charge on retry
Type: bug
Problem: Customers on the billing page get charged twice when a slow network
causes them to double-click "Pay" before the first request resolves.
Who is affected: any customer checking out on a mobile connection
Known:
- POST /api/charges has no idempotency key
Assumed:
- [ASSUMED] This only happens on the client-side retry, not the payment gateway
Affected surfaces:
- app/billing/pay-button.tsx — fires request on click, no debounce
- lib/payments/charge.ts — creates a new charge record per call
Out of scope (explicit):
- Refund flow for already-duplicated charges
Open questions:
1. Should the idempotency key be per-cart or per-session?
```
</details>

### `agent-registry/` — example roster

The bundled [`AGENTS.md.template`](skills/agent-registry/AGENTS.md.template) ships
with a software development roster as a worked example. Swap it for whatever
specialists your project actually needs.

| Agent | Routes here for | Status in template |
|-------|------------------|---------------------|
| `BACKEND` | REST/GraphQL endpoints, business logic, data models, background jobs, third-party integrations. | Fully defined — has its own `BACKEND_AGENT.md` |
| `FRONTEND` | UI components, client-side state, styling, accessibility, browser behavior. | Routing target only — instruction file not yet written |
| `DATA` | Schema design, migrations, queries, data pipelines, analytics. | Routing target only |
| `SECURITY` | AuthN/authZ, secrets handling, dependency vulnerabilities, threat modeling. | Routing target only |
| `DEVOPS` | CI/CD, infrastructure, deployment, observability, incident response. | Routing target only |

"Routing target only" means the template already routes requests to that name,
but you need to add its `<AGENT_NAME>_AGENT.md` (see section 6, "Future
Agents", in the template) before it does real work — otherwise the closest
existing agent handles it and the gap gets flagged.

<details>
<summary>Sample: routing a request</summary>

```
Request: "Add validation and a service method for updating a user's email"
→ single discipline: BACKEND
→ BACKEND reads AGENTS.md + its own instruction file + PROJECT.md/CONVENTIONS.md
→ produces the endpoint, validation and tests

Request: "Add an endpoint that lets users export their data as CSV"
→ spans multiple disciplines:
  1. DATA     → confirm schema, indexes, query shape for the export
  2. BACKEND  → implement the endpoint, pagination, CSV generation (primary agent)
  3. SECURITY → check authorization (own data only), rate limiting, injection risk
```
</details>

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
