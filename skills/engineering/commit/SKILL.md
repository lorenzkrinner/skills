---
name: commit
description: Use when committing changes to git
---

# Commit changes to git

You must end by running a real `git commit`. A summary is a failure.

## Scope
- Commit only files changed in the current conversation. If the user names paths, use only those. Only commit the full working tree if the user says "commit all" or equivalent.
- If you can't separate conversation changes from unrelated working-tree changes, stop and ask which paths to include. Never stage everything to be safe.
- Never stage `.env`, keys, or credential files.

## Split into focused commits
- Keep each commit focused on one purpose that can be reviewed and reverted independently.
- Separate unrelated documentation, reusable components, features, and fixes into their own commits.
- Keep supporting code, tests, dependencies, and documentation with the change they support.
- Each commit should build and pass its relevant checks.
- If the scoped changes contain several purposes, make several commits in dependency order.

## Inspect current state
Run these first:
- `git status --short`
- `git diff`
- `git diff --cached`

## Process
Some examples are javascript or typescript specific, when committing other languages, use their equivalent.

1. **Review** the scoped diff for real defects only: wrong logic, broken contracts, obvious edge cases, unsafe side effects. Ignore style.
   - If you find a **critical** bug, stop without committing and reply with only this table:
     | Severity | Where | Problem | Suggested fix |
     |---|---|---|---|
     | critical | `path:line` | one line | one line |
   - Medium/low: note in output, still commit.
2. **Deslop** the scoped changes. Remove:
   - Comments a human wouldn't add or that clash with the file
   - Extra defensive checks or try/catch abnormal for that area
   - `any` casts over types
   - Style inconsistent with the file
3. **Commit** each focused group from "Split into focused commits":
   Prefix: `feat:` `fix:` `refactor:` `docs:` `chore:`. Body only if the change is large.

## Do not
- Write session handoffs, recaps, or status reports.
- Skip the commit because of unrelated bugs elsewhere.

## Output
Reply with only:
```
Review: clean | <one-line note>
Deslop: <one sentence> | nothing
Commit: <hash> — <subject>   (one line per commit)
```
per commit or a review table if blocked. Keep one whitespace per commit if you have multiple.
