---
name: setup-lorenz-krinner-skills
description: Set up Lorenz Krinner's repository workflow, skills, documentation, and optional Entire session tracking. Use when asked to initialize or repair this setup.
disable-model-invocation: true
---

# Setup Lorenz Krinner Skills

Set up the current Git repository. Preserve existing project instructions and conventions. The Lorenz `AGENTS.md` skeleton is required. Merge existing content into it. Do not wipe and replace.

## 1. Inspect

Read the repository before asking questions or editing files:

- Root `AGENTS.md`, `CLAUDE.md`, `README.md`, `CONTEXT.md`, and `WORKLOG.md`
- `docs/agents/`, `docs/architecture/`, and `docs/adr/`
- Git remotes, default branch, active branch, and integration-branch candidates
- Package, workspace, service, application, CI, and verification configuration
- Existing agent skill directories and Entire configuration

Integration-branch candidates include names such as `dev`, `development`, and `testing`, plus any integration branch named in CI or package scripts. Prefer an existing candidate used by this repo. Do not assume the name is `development`.

Infer the repository state. Do not ask the user to describe information that the repository provides.

## 2. Ask Questions

Ask only the questions this skill owns. The delegated `setup-matt-pocock-skills` workflow still owns and asks its repository configuration questions. Tool permission or authentication prompts may also occur when required by the environment.

### Entire

Use the environment's available question or user-input tool to ask:

> Do you want to set up Entire for session tracking?

Offer `Yes` and `No`.

### Integration branch

If inspection finds one clear integration branch, use it. Do not ask.

If none exists, or more than one candidate is plausible, ask once which branch is the integration branch. Record that name and use it everywhere this skill writes workflow text. Create the branch from `main` only when it is missing. Do not rename an existing branch. Do not push unless the user already asked for remote setup. If unclear, ask the user.

### Existing `AGENTS.md` content

If root `AGENTS.md` is missing or empty, skip this question.

If it has content beyond a blank Lorenz skeleton, inventory every heading or block. For each block, propose one fate:

- **keep** in root `AGENTS.md` (merged under or after the required Lorenz skeleton)
- **move** into a `docs/agents/` file (create or update that file; add a pointer when useful)
- **drop** only with explicit user approval

Ask once how to handle the non-template blocks. Default posture: keep repo-specific operating rules. Never silently delete a block.

## 3. Install Skills

Inspect the current `mattpocock/skills` source. Select every skill whose `SKILL.md` is under either of these folders, and no others:

- `skills/engineering/`
- `skills/productivity/`

Install the selected names into the universal target:

```bash
npx skills@latest add mattpocock/skills --skill <selected-skill-names> --agent universal --yes
```

Do not install skills from another Matt Pocock folder. Build the selected list from the current upstream tree instead of assuming that the repository's skill list is static.

Install the workflow skills from this repository into the same target:

```bash
npx skills@latest add lorenzkrinner/skills --skill what-next consolidate --agent universal --yes
```

If Entire was selected, install all Entire skills:

```bash
npx skills@latest add entireio/skills --skill '*' --agent universal --yes
```

Do not install Entire skills when the user selected `No`. Preserve any existing Entire configuration unchanged.

Use only `.agents/skills` as the project skill directory. Remove a generated `agent/skills` directory when this setup created it. Preserve pre-existing files that were not created by this setup.

Run the installed `setup-matt-pocock-skills` workflow. Let that skill own issue tracker, triage label, `CONTEXT.md`, and ADR setup. Do not duplicate its questions or files.

## 4. Configure Repository Files

Read [references/repository-files.md](references/repository-files.md). The Lorenz skeleton there is required. Apply it after `setup-matt-pocock-skills` finishes so that delegated setup cannot leave a different structure behind.

### Orphan checklist

Before writing root `AGENTS.md`, complete this checklist:

1. List headings and durable blocks in the old `AGENTS.md` (if any).
2. List headings in the Lorenz skeleton.
3. Mark each old block as **keep**, **move** (with destination path), or **drop** (user-approved only).
4. Do not write until every old block has a fate.

### Product description

Fill `## Product Description` from existing product text in `AGENTS.md`, `README.md`, or `CONTEXT.md` when present. Use `<add description>` only when none exists. Do not replace known product text with a placeholder.

### Merge and approve `AGENTS.md`

1. Build the merged `AGENTS.md`: required Lorenz skeleton first, then kept project sections, with moved content written to destination docs and pointed to when useful.
2. Do not paraphrase the required Lorenz headings. Do not retain Matt Pocock's `## Agent skills` section. Convert its information into pointer bullets under the relevant `## Sources of Truth` subsection. Add only pointers to files that exist.
3. Substitute the chosen integration-branch name wherever the skeleton shows `<integration-branch>`.
4. If the old `AGENTS.md` was non-empty, show the **full final draft** in a fenced code block and wait for approval before writing. If it was empty or missing, write without that review pause.
5. Create or repair root `WORKLOG.md` with the standard empty headings.
6. Create `docs/agents/workflow.md` using the chosen integration-branch name.
7. Create or update `docs/architecture/` documents for important flows. Prefer moving existing architecture docs into `docs/architecture/` over duplicating them. Update live references after a move.
8. Add one direct pointer for every architecture document to the root `AGENTS.md` architecture section.
9. Update the relevant architecture document when the setup changes a documented flow.
10. Add or update the concise `README.md` product description and optional Entire setup section.

Do not document worktrees, clones, cloud environments, or another parallel execution mechanism. The workflow defines outcomes, not where work runs.

## 5. Configure Entire When Selected

If the user selected `No`, make no Entire-related changes. Do not remove existing Entire configuration or documentation.

If the user selected `Yes`:

1. Check the current official Entire CLI installation documentation.
2. Install the stable Entire CLI for the current operating system when `entire` is unavailable.
3. Verify the CLI installation with `entire version`.
4. Create or update `docs/agents/session-tracking.md` with the deferred enable instructions and privacy notes.
5. Add its pointer to `AGENTS.md`.
6. Add CLI installation instructions to `README.md`.

Never run `entire enable` for the user and never answer its wizard prompts. Do not pause or wait for the user. Finish the complete repository setup first.

When all other setup is complete, end the response with this small block:

````markdown
**One last step.**

Run this command to set up Entire to your liking:

```bash
entire enable
```
````

## 6. Validate

Check every completion criterion:

- Matt Pocock's setup is complete.
- Required workflow skills are installed.
- `AGENTS.md` starts with `# AGENTS.md`, followed by `## Product Description`, and includes the required Lorenz section order.
- Product description is real existing text when available; otherwise `<add description>`.
- `AGENTS.md` has one `## Sources of Truth` section with `### Architecture`, `### Product Context`, and `### Agent Workflow` subsections.
- Each source-of-truth subsection uses a flat pointer list.
- `AGENTS.md` contains no nested Matt Pocock configuration headings.
- Every pre-existing `AGENTS.md` block was kept, moved, or explicitly dropped.
- When the old `AGENTS.md` was non-empty, the final draft was shown in a code block and approved before write.
- Workflow docs use the chosen integration-branch name, not a hard-coded `development`.
- `AGENTS.md` points directly to every architecture document.
- `WORKLOG.md` contains the required headings.
- `docs/agents/workflow.md` contains integration and work-log rules.
- `README.md` contains a product description and adds the Entire CLI setup only when selected.
- Skills are installed only under `.agents/skills`; no setup-created `agent/skills` remains.
- Entire is unchanged when declined, or its CLI is installed and repository enablement is deferred when selected.
- Existing unrelated documentation remains intact.

Report created files, modified files, installed skills, and branch changes. Add the final Entire block when selected. Do not commit unless the user explicitly asks.
