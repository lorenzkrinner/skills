---
name: setup-repo
description: Set up repository workflow, skills, documentation, and optional Entire session tracking. Use when the user asks to initialize or repair this repository setup.
disable-model-invocation: true
---

# Setup Repo

Set up the current Git repository. Preserve existing project instructions and conventions unless they conflict with an explicit requirement below.

## 1. Inspect

Read the repository before asking questions or editing files:

- Root `AGENTS.md`, `CLAUDE.md`, `README.md`, `CONTEXT.md`, and `WORKLOG.md`
- `docs/agents/`, `docs/architecture/`, and `docs/adr/`
- Git remotes, default branch, active branch, and existing `development` branch
- Package, workspace, service, application, CI, and verification configuration
- Existing agent skill directories and Entire configuration

Infer the repository state. Do not ask the user to describe information that the repository provides.

## 2. Ask One Question

Use the agent's user-question tool to ask:

> Do you want to set up Entire for session tracking?

Offer `Yes` and `No`. This skill asks no other workflow question. The delegated `setup-matt-pocock-skills` workflow still owns and asks its repository configuration questions. Tool permission or authentication prompts may also occur when required by the environment.

## 3. Install Skills

Install all Matt Pocock skills for all agents supported by the Skills CLI:

```bash
npx skills@latest add mattpocock/skills --all
```

Install the workflow skills from this repository for all supported agents:

```bash
npx skills@latest add lorenzkrinner/skills --skill what-next consolidate --agent '*' --yes
```

If Entire was selected, install all Entire skills:

```bash
npx skills@latest add entireio/skills --all
```

Do not install Entire skills when the user selected `No`. Preserve any existing Entire configuration unchanged.

Run the installed `setup-matt-pocock-skills` workflow. Let that skill own issue tracker, triage label, `CONTEXT.md`, and ADR setup. Do not duplicate its questions or files.

## 4. Configure Repository Files

Read [references/repository-files.md](references/repository-files.md). Apply its templates as managed sections, adapted to the repository:

1. Create or update root `AGENTS.md`.
2. Create or repair root `WORKLOG.md` with the standard empty headings.
3. Create `docs/agents/workflow.md`.
4. Create `docs/architecture/overview.md` and focused architecture documents for important flows that can be verified from the code.
5. Add one direct pointer for every architecture document to the root `AGENTS.md` architecture section.
6. Update the relevant architecture document when the setup changes a documented flow.
7. Add or update concise `README.md` sections for architecture and workflow.

Do not document worktrees, clones, cloud environments, or another parallel execution mechanism. The workflow defines outcomes, not where work runs.

Record the fixed integration flow in `docs/agents/workflow.md`: ticket branches merge into `development`; `development` merges into `main` only after tests and live verification pass.

If `development` does not exist, create it from `main` without changing the current branch. Do not push it unless the user already asked for remote setup.

## 5. Configure Entire When Selected

If the user selected `No`, make no Entire-related changes. Do not remove existing Entire configuration or documentation.

If the user selected `Yes`:

1. Check the current official Entire CLI installation documentation.
2. Install the stable Entire CLI for the current operating system when `entire` is unavailable.
3. Enable Entire for the current agent and add other supported agents detected in the repository.
4. Create or update `docs/agents/session-tracking.md` with repository-specific configuration and privacy notes.
5. Add its pointer to `AGENTS.md`.
6. Add CLI installation and `entire status` instructions to `README.md`.
7. Verify setup with `entire status`.

Do not manually write Entire hook files. Use the Entire CLI.

## 6. Validate

Check every completion criterion:

- Matt Pocock's setup is complete.
- Required workflow skills are installed.
- `AGENTS.md` points directly to every architecture document.
- `WORKLOG.md` contains the required headings.
- `docs/agents/workflow.md` contains integration and work-log rules.
- `README.md` links to architecture and agent workflow documentation.
- Entire is unchanged when declined, or enabled and healthy when selected.
- Existing unrelated documentation remains intact.

Report created files, modified files, installed skills, branch changes, and any setup that still requires human authentication. Do not commit unless the user explicitly asks.
