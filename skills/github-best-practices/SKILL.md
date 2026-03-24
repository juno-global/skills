---
name: github-best-practices
description: GitHub best practices for commits, pull requests, and CLI usage. Use when creating commits, opening PRs, pushing branches, or working with GitHub repositories.
---

# GitHub Best Practices

## 1. PR Templates

Always check for a PR template before creating a pull request:

```bash
ls .github/
# Look for: PULL_REQUEST_TEMPLATE.md or PULL_REQUEST_TEMPLATE/ directory
```

If a template exists, use its structure when writing the PR body. Never skip sections — fill them out with relevant information. If a section is not applicable, note that explicitly rather than omitting it.

## 2. Open PRs as Drafts First

Always create pull requests as drafts unless the user explicitly asks for a ready-for-review PR:

```bash
# Correct
gh pr create --draft --title "..." --body "..."

# Only use this when the user explicitly requests it
gh pr create --title "..." --body "..."
```

Drafts signal that the work is in progress and not yet ready for review. This avoids accidentally requesting reviews prematurely.

## 3. Never Commit to a Merged PR's Branch

Before committing, check if there is an open PR for the current branch and whether it has already been merged:

```bash
# Check the current branch's PR status
gh pr view --json state,mergedAt,title

# Or list open PRs for the current branch
gh pr list --head $(git branch --show-current)
```

- If the PR is **merged**, do NOT push new commits to that branch. Create a new branch instead.
- If no PR exists yet, proceed normally.
- If a PR is open and not yet merged, committing and pushing is fine.

## 4. Match the Repo's Commit Format

Before writing a commit message, inspect recent commits to understand the project's conventions:

```bash
git log --oneline -10
```

Common formats to look for:

- **Conventional commits**: `feat(scope): description`, `fix: description`, `chore: description`
- **Simple imperative**: `Add feature`, `Fix bug`, `Update docs`
- **Issue references**: `Fix #123: description`
- **Custom formats**: Anything else the team uses

Match whatever format is already in use. Do not introduce a new style unless asked.

## 5. Prefer gh CLI, Then MCP Tools

When working with GitHub, follow this priority order:

1. **`gh` CLI** — use if available (`which gh` to check). Prefer it for all GitHub operations: creating PRs, listing issues, checking PR status, etc.
2. **MCP/tool integrations** — if `gh` is not available, check whether a GitHub MCP server or tool is connected (e.g., a GitHub Composio tool).
3. **REST API via curl** — last resort if neither of the above is available.

```bash
# Check if gh is available
which gh

# Check if gh is authenticated
gh auth status
```

Always confirm `gh` is authenticated before using it. If not authenticated, fall back to available MCP tools.
