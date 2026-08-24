---
name: what-next
description: Assess project state and recommend the next work. Use when the user asks what to do next.
disable-model-invocation: true
---

# What Next

Assess the current project without changing it.

## Inspect

Read the repository's configured sources of truth:

- Root `AGENTS.md`, `CONTEXT.md`, and `WORKLOG.md`
- `docs/agents/issue-tracker.md`, `docs/agents/triage-labels.md`, and `docs/agents/workflow.md`
- Relevant files under `docs/architecture/` and `docs/adr/`
- Open tickets, dependency edges, assignments, and status in the configured tracker
- Open pull requests and their checks
- Local and remote branches, especially `development` and `main`
- Current diffs only when they affect project readiness

Use Entire history when it is configured and useful. Do not require it.

## Assess

Identify:

- Unblocked tickets that are ready to implement
- Work already in progress
- Work waiting for review, checks, live verification, or integration
- Blockers and missing decisions
- Shared contracts or files that make parallel work unsafe
- The next change that unlocks the most useful downstream work

Prefer small tracer-bullet work over broad horizontal tasks. Respect declared dependency edges and the repository's `development` to `main` integration flow.

## Respond

Lead with one recommended next action and why it is next. Then list, when relevant:

- Other work that can proceed independently
- Blocked work and the exact unblocker
- Work ready for review or integration
- Risks that require human coordination

Use ticket identifiers and links. Keep the answer concise.

Do not claim tickets, edit files, update the tracker, create branches, or merge work. A follow-up explicit order is required for changes.
