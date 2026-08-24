# Repository Files

Use these as managed sections. Preserve unrelated content and adapt labels and paths to the repository. Do not add a pointer for a file that does not exist.

## `AGENTS.md`

```markdown
## Workflow

- Use tickets as the source of truth for planned work.
- Merge ticket branches into `development`.
- Merge `development` into `main` only after tests and live verification pass.
- Run the `consolidate` skill before integration.

## Work Log

Maintain `WORKLOG.md` during implementation. If it is missing, create it with the required headings. Follow `docs/agents/workflow.md#work-log`.

## Architecture

- System overview: `docs/architecture/overview.md`
- [Verified flow]: `docs/architecture/<flow>.md`

Update the relevant architecture document when a change affects a documented flow. Add every new architecture document to this list.

## Project Context

See `CONTEXT.md` for domain terms and system boundaries.

## Agent Workflow

See `docs/agents/workflow.md` for the delivery workflow.

## Agent Configuration

See `docs/agents/issue-tracker.md` for the issue tracker.
See `docs/agents/triage-labels.md` for ticket states.
See `docs/agents/domain.md` for domain documentation.
```

When Entire is enabled, add this line under `## Agent Workflow`:

```markdown
See `docs/agents/session-tracking.md` for Entire session tracking.
```

Omit Matt Pocock pointers for files that its setup did not create.

## `docs/agents/session-tracking.md`

Create this file only when Entire setup is selected:

```markdown
# Session Tracking

## Tool

This repository uses Entire to link agent sessions to Git commits.

## Setup

Document the repository's enabled agent integrations and committed Entire settings.

## Checkpoints

Make coherent commits at useful boundaries. Entire stores session metadata on `entire/checkpoints/v1` and links checkpoints to commits.

## Handoffs

Reference the ticket, branch, commit, and relevant Entire checkpoint when handing work to another person or agent.

## Privacy

Session transcripts can contain sensitive context. Record whether checkpoints use the code remote or a separate private checkpoint remote. Secret redaction is best-effort.

## Verification

Run `entire status` in the active repository.
```

## `WORKLOG.md`

```markdown
# Work Log

## Implementation Decisions

## Spec Deviations

## Failed Approaches

## Shared Contract Changes

## Open Concerns
```

## `docs/agents/workflow.md`

```markdown
# Delivery Workflow

## Work

Use tickets as the source of truth for planned work. Claim a ticket before implementation when the tracker supports assignment. Surface changes that can affect other active tickets or branches.

## Integration

Merge ticket branches into `development`. Merge `development` into `main` only after tests and live verification pass.

Run the `consolidate` skill before integration.

## Work Log

Maintain `WORKLOG.md` while implementing work. Create it with the standard headings when it is missing.

Record important implementation decisions, specification deviations, meaningful failed approaches, shared contract changes, and open concerns.

Before integration, move durable information to the correct source of truth, clear the content under every work-log heading, and preserve the file and all headings.

Use subagents for independent work when delegation saves time or protects the main context. Handle simple work directly.

## Architecture

Update the relevant file under `docs/architecture/` when a change affects a documented flow. Add a direct pointer to every new architecture document in root `AGENTS.md`.
```

## Architecture

Create `docs/architecture/overview.md` as a concise map:

```markdown
# Architecture Overview

## System

## Components

## Main Flows

## Data

## External Systems

## Architecture Documents
```

Create a focused architecture document only when the code provides enough evidence to document the flow accurately:

```markdown
# Flow Name

## Purpose

## Entry Points

## Components

## Flow

## Data

## Interfaces

## Failure Modes

## File Locations

## Related Decisions
```

Architecture documents describe the current system. ADRs explain why durable decisions were made.

## `README.md`

Add or update concise sections. Preserve existing setup and product documentation.

```markdown
## Branches

Ticket branches merge into `development`. `development` merges into `main` after tests and live verification.

## Architecture

Read `docs/architecture/overview.md` for the system overview. Detailed flows live under `docs/architecture/`.

## Agent Workflow

Repository instructions live in `AGENTS.md`.
```

When Entire is enabled, add:

````markdown
## Session Tracking

This repository uses Entire to track agent sessions.

Install the stable CLI on macOS or Linux:

```bash
curl -fsSL https://entire.io/install.sh | bash
```

On Windows, follow the current Scoop installation instructions in the official Entire documentation.

Check the repository setup:

```bash
entire status
```

See `docs/agents/session-tracking.md` for repository-specific details.
````
