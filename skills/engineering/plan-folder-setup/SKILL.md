---
name: plan-folder-setup
description: Create or maintain repository plan folders under plans/<slug>/ with a plan.md, optional plan.html review artifact, and implementation-details.md decision log. Use when a user asks to create a plan, planning directory, implementation notes, reviewable plan HTML, or to document agent plan structure.
disable-model-invocation: true
---

# Plan Folder Setup

Use this workflow when creating or updating durable planning artifacts in this repository.

## Structure

Create one directory per plan:

```text
plans/<plan-slug>/
|-- plan.md
|-- plan.html
`-- implementation-details.md
```

`plan.html` is optional unless the user asks for an HTML review artifact. Prefer lowercase kebab-case directory names that describe the product or engineering initiative.

## Files

`plan.md` is the human-readable plan. Include:

- Problem statement
- Goals and non-goals
- Current-state findings with relevant file references
- Proposed architecture or workflow
- Implementation phases
- Testing and rollout plan
- Risks and open questions
- Source links when research influenced the plan

`plan.html` is a review-focused rendering of the plan. Keep it self-contained with inline CSS. It does not need to duplicate every line from `plan.md`, but it must preserve the decisions, phases, risks, and links needed for review.

`implementation-details.md` is a living decision log for the implementation agent. Start it when the plan is created and update it during implementation. Record:

- Decisions made
- Files changed
- Behavior intentionally changed
- Deviations from `plan.md`
- Commands run and verification results
- Unresolved risks or follow-up work

## Workflow

1. Create the plan directory under `plans/`.
2. Add or update `plan.md`.
3. Add `plan.html` when requested or useful for review.
4. Add `implementation-details.md` with an initial blank decision log.
5. Update root `AGENTS.md` if the repository plan structure changes.
6. Keep implementation notes factual and append-only where practical, so the user can audit what changed.

