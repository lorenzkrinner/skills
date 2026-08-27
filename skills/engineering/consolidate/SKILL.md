---
name: consolidate
description: Preserve durable implementation context and reset WORKLOG.md. Use before integrating completed work.
disable-model-invocation: true
---

# Consolidate

Consolidate the current implementation before it is integrated. Do not commit, merge, or push.

## Read

Read:

- The implemented ticket or specification
- `WORKLOG.md`
- The current diff and commits since the integration base
- `CONTEXT.md`
- Relevant files under `docs/architecture/` and `docs/adr/`
- The issue tracker and domain documentation rules under `docs/agents/`
- Root `AGENTS.md`

## Preserve

Move each durable work-log item to one authoritative destination:

- Durable architectural or domain decision: use the repository's ADR and domain-modeling rules.
- Current system flow, boundary, interface, dependency, or file location: update the relevant architecture document.
- New architecture document: add a direct pointer under the root `AGENTS.md` architecture section.
- Specification deviation: update or comment on the originating ticket when the configured tracker permits it.
- Follow-up work or unresolved concern: create or update a ticket without duplicating existing work.
- Failed approach: preserve it only when it prevents likely repetition; otherwise Entire or Git history is sufficient.

Keep architecture documents current-state only. Keep reasons for durable decisions in ADRs.

Tell the human about shared contract, interface, schema, migration, or behavior changes that can affect active branches. Do not silently resolve cross-branch coordination risk.

## Reset Work Log

Ensure `WORKLOG.md` exists and contains at least this heading structure:

```markdown
# Work Log

## Implementation Decisions

## Spec Deviations

## Failed Approaches

## Shared Contract Changes

## Open Concerns
```

Remove all bullets and paragraphs under every heading after their durable content has been preserved or deliberately discarded. Preserve the file, the standard headings, and any repository-specific headings.

## Verify

Finish only when:

- Every work-log item has a destination or an explicit discard reason.
- Relevant architecture documents match the implemented system.
- Every architecture document has a direct `AGENTS.md` pointer.
- Follow-up work is represented in the configured tracker.
- `WORKLOG.md` contains only its preserved headings and blank lines.
- Cross-branch effects have been surfaced to the human.

Report what moved, what was discarded, and which files or tickets changed.
