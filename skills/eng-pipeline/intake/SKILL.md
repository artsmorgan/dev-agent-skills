---
name: intake
description: Turn a vague issue, bug report, Slack message or feature request into a bounded problem statement (intake.md). Use this whenever a new piece of work arrives, when someone says "we need X", "there's a bug in Y", "can we add Z", or before writing any spec. Use even if the request looks clear — it is the gate for scope.
---

# Intake — Stage 1 of 9

Read `_shared/project-context.md` first.

**Goal:** bounded problem, no solutions.
**Input:** issue / message / bug report. **Output:** `docs/work/<ticket>/intake.md`.

## Do
1. Restate the problem in one sentence: *who* has *what* pain, *when*.
2. Classify: `feature | bug | tech-debt | spike`.
3. Separate known from assumed. Tag assumptions `[ASSUMED]`.
4. Identify affected surfaces (modules, tables, endpoints, screens) **by reading the code**, not guessing.
5. Ask at most 3 clarifying questions. If unanswered, proceed with tags.

## Do not
Propose architecture, estimate, or write code.

## Template
```md
# Intake — <ticket> <title>
Type: feature | bug | tech-debt | spike
Problem: <one sentence>
Who is affected: <role / segment>
Known:
- …
Assumed:
- [ASSUMED] …
Affected surfaces:
- path/to/module — why
Out of scope (explicit):
- …
Open questions:
1. …
```

## DONE when
Problem is one sentence · out-of-scope is explicit · every assumption tagged.

Next stage: `spec/`.
