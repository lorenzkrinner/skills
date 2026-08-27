---
name: finish-issue
description: Squash-merge the PR, delete the branch, close the issue, and link the PR. Use when finishing delivered ticket work.
disable-model-invocation: true
---

# Finish Issue

Close out a delivered ticket. Prefer one PR and one issue. Do not start this skill until the work is ready to land.

## Resolve Targets

Identify:

1. The issue number
2. The pull request number or URL
3. The head branch name

Infer them from the conversation, the current branch, open PRs for that branch, and issue links in the PR body. Ask only when a target is ambiguous.

Read `docs/agents/issue-tracker.md` or a equivalent file when present for tracker conventions.

## Preconditions

Continue only when all of these hold:

- The PR is open, or already merged
- CI on the PR head is green, or the user explicitly accepts merging with known failures. If unsure ask the user first
- The PR base is the intended integration branch

Stop and report when a precondition fails.

## Finish

Run these steps in order. Skip a step only when its completion criterion is already true.

1. **Link issue to PR.** Ensure the PR body names the issue with a closing keyword such as `Closes #<n>` or `Fixes #<n>`. Edit the PR body when the keyword is missing.
2. **Link PR to issue** Link the PR to the issue
3. **Squash-merge.** If the PR is still open, squash-merge it:
   ```bash
   gh pr merge <pr> --squash --delete-branch