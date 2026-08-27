# Repository Files

Use these as managed structures. Preserve unrelated content in files other than root `AGENTS.md` unless the user approved a move or drop. Do not add a pointer for a file that does not exist.

## `AGENTS.md`

The Lorenz skeleton below is required. It is a merge floor, not a full-file overwrite.

Required order at the top:

1. `# AGENTS.md`
2. `## Product Description`
3. `## Workflow`
4. `## Work Log`
5. `## Sources of Truth` with `### Architecture`, `### Product Context`, and `### Agent Workflow`

After that skeleton, keep user-approved project sections from the old file. Do not retain Matt Pocock's nested `## Agent skills` block; convert it into Sources of Truth pointers.

Variable content:

- Product description text (existing repo text when available; otherwise `<add description>`)
- Integration-branch name in Workflow bullets (`<integration-branch>`)
- Architecture pointer bullets for verified architecture documents
- Pointers for agent files that actually exist
- The optional Entire pointer
- Kept project sections after the skeleton

### Product description

Prefer existing product text from root `AGENTS.md`, `README.md`, or `CONTEXT.md`. Use `<add description>` only when none exists. Never replace known product text with a placeholder.

### Orphan checklist and approval

Before writing:

1. Inventory old `AGENTS.md` headings and durable blocks.
2. Mark each as keep, move (with path), or drop (user-approved only).
3. If the old file was non-empty, show the full final draft in a fenced code block and wait for approval.

### Skeleton

Replace `<integration-branch>` with the chosen branch name (`dev`, `development`, `testing`, or another name this repo uses).

```markdown
# AGENTS.md

## Product Description

<add description>

## Workflow

- Use tickets as the source of truth for planned work.
- Merge ticket branches into `<integration-branch>`.
- Merge `<integration-branch>` into `main` only after tests and live verification pass.
- Use the `consolidate` skill before integration.

## Work Log

Maintain `WORKLOG.md` during implementation. If it is missing, create it with the required headings. Follow `docs/agents/workflow.md#work-log`.

## Sources of Truth

### Architecture

- System overview: `docs/architecture/overview.md`
- [Verified flow]: `docs/architecture/<flow>.md`

Update the relevant architecture document when a change affects a documented flow. Add every new architecture document to this list.

### Product Context

- Domain model: `CONTEXT.md`
- Domain documentation rules: `docs/agents/domain.md`

### Agent Workflow

- Delivery workflow: `docs/agents/workflow.md`
- Issue tracker: `docs/agents/issue-tracker.md`
- Ticket states: `docs/agents/triage-labels.md`
```

When Entire is enabled, add this line under `### Agent Workflow`:

```markdown
- Entire session tracking: `docs/agents/session-tracking.md`
```

Omit Matt Pocock pointers for files that its setup did not create.

## `docs/agents/session-tracking.md`

Create this file only when Entire setup is selected:

```markdown
# Session Tracking

## Tool

This repository uses Entire to link agent sessions to Git commits.

## Setup

Install the Entire CLI during repository setup. Run `entire enable` after repository setup to choose agent integrations and repository settings through Entire's wizard.

## Checkpoints

Make coherent commits at useful boundaries. Entire stores session metadata on `entire/checkpoints/v1` and links checkpoints to commits.

## Handoffs

Reference the ticket, branch, commit, and relevant Entire checkpoint when handing work to another person or agent.

## Privacy

Session transcripts can contain sensitive context. Record whether checkpoints use the code remote or a separate private checkpoint remote. Secret redaction is best-effort.

## Verification

Run `entire status` after `entire enable` completes.
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

Replace `<integration-branch>` with the chosen branch name.

```markdown
# Delivery Workflow

## Work

Use tickets as the source of truth for planned work. Claim a ticket before implementation when the tracker supports assignment. Surface changes that can affect other active tickets or branches.

## Integration

Merge ticket branches into `<integration-branch>`. Merge `<integration-branch>` into `main` only after tests and live verification pass.

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

Prefer moving existing architecture docs into `docs/architecture/` over creating duplicates. Update live references after a move.

Create `docs/architecture/overview.md` as a concise map when no overview exists yet:

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

Preserve useful existing product and setup content. Fill `## Product Description` from existing product text when present. Use `<add description>` only when none exists. Add missing managed sections without copying architecture or workflow documentation into the README:

````markdown
# README.md

## Product Description

<add description>

## Setup

### Set Up Entire

This repository uses Entire for agent session tracking. Install the stable CLI before working with an agent.

On macOS:

```bash
brew tap entireio/tap
brew trust entireio/tap
brew install --cask entire
```

On Linux:

```bash
curl -fsSL https://entire.io/install.sh | bash
```

On Windows, follow the current Scoop installation instructions in the official Entire documentation.
````

Add `## Setup` and `### Set Up Entire` only when Entire setup is selected. Do not add README sections for branches, architecture, agent workflow, or session-tracking details; those belong in `docs/` and `AGENTS.md`.
