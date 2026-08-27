---
name: finish-issue
description: Merge a ticket PR, attach it as the GitHub Development closer, and close the issue.
disable-model-invocation: true
---

# Finish Issue

Close one GitHub issue with one squash-merged PR. Read `docs/agents/issue-tracker.md`.

## Terms

**Development** is the GitHub issue sidebar section that lists the PR which closes the issue.

## Rules

- Prefer one PR and one issue.
- Put `Closes #<issue>` in the PR body.
- Also attach the PR as a Development closing reference. A closing keyword is not enough unless the merge target is the default branch.
- Squash-merge and delete the head branch.
- Close the issue yourself

## Closing keywords vs Development

`Closes #n` / `Fixes #n` / `Resolves #n` auto-link and auto-close only when the PR merges into the repo default branch (`main` here).

On a PR into a non-default branch, the keyword is only a mention. It does not fill Development and does not close the issue. Merging that integration branch into `dev`/`main` later is a different PR and does not backfill this one as the closer.

`addCloseIssueReferences` fills Development for any base. Manually linked PRs still auto-close only on a default-branch merge, so close the issue yourself after a non-default merge.

## Steps

1. Resolve the issue number, PR number/URL, head branch, PR base, and GraphQL node ids (`gh issue view` / `gh pr view --json id`). Stop if more than one PR fits, or if no PR exists (use `create-pr`).

2. Ship only if the PR is open or already merged, not a draft, checks are green (or the user accepts failures, ask first if CI failed), and the base is the intended integration branch. Do not retarget it.

3. Append `Closes #<issue>` to the PR. Keep the rest of the body.

4. List the PR:

   ```bash
   ISSUE_ID="$(gh issue view <issue> --json id --jq .id)"
   PR_ID="$(gh pr view <pr> --json id --jq .id)"
   gh api graphql -f query='mutation($issueId:ID!, $prId:ID!) {
     addCloseIssueReferences(input: {issueId: $issueId, pullRequestIds: [$prId]}) {
       issue { closedByPullRequestsReferences(first: 10, includeClosedPrs: true) { nodes { number url } } }
     }
   }' -f issueId="$ISSUE_ID" -f prId="$PR_ID"
   ```

   Use the GraphQL `id`, not the numeric database id. Repeat once per issue if several issues share the PR. Confirm the PR number is in `closedByPullRequestsReferences`.

5. Squash-merge the PR: `gh pr merge <pr> --squash --delete-branch`. On `403`, give the user that exact command and wait. After they confirm the merge, continue.

6. Close the issue: `gh issue close <issue> --comment "Shipped in <pr-url>."` This is expected when the merge target is not `main`.

7. Delete the branch `git push origin --delete <head-branch>`. Delete only the PR head. Leave `main`, `dev`, and long-lived integration branches.

On any write `403` (merge, GraphQL, close, delete), give the exact command and wait. Do not retry `403`. Do not open a second PR or issue to finish the first pair.

## Report

Issue closed, PR merged, Development shows this PR, whether you closed the issue yourself, branch deleted, any command the user had to run.