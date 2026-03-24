---
name: linear-workflow
description: Linear issue management best practices. Use when creating, updating, or working with Linear tasks, issues, subtasks, or projects.
---

# Linear Workflow Best Practices

## Creating Issues

### Status on Creation

- **Features** → always create in **Backlog**
- **Bugs** → always create in **Triage**

Never create issues directly in "In Progress" or "Done". Let the team move them through the workflow.

### Issue Body

The issue body is the single source of truth for scope and intent. When creating or updating an issue:

- Write a clear **problem statement** or **goal**
- Include a **task plan** — a numbered list of the specific steps needed to complete the work
- Add **acceptance criteria** where relevant
- Include links to designs, specs, or related issues

**Do not put the task plan in comments.** Comments are for implementation updates only (see below).

Example body structure:

```
## Goal
Brief description of what this achieves and why.

## Task Plan
1. Update the database schema to add X column
2. Add migration for existing records
3. Expose new field via API endpoint
4. Update frontend to display the field
5. Write tests

## Acceptance Criteria
- [ ] Users can see X in the UI
- [ ] API returns X in the response
- [ ] Existing data is migrated correctly
```

## Breaking Up Complex Work

Use **subtasks** to decompose complex issues into concrete units of work:

- Create subtasks when a single issue spans multiple independent pieces (e.g., backend + frontend + migrations)
- Each subtask should be completable independently
- Subtasks can be assigned to different people if the work is parallelizable
- Keep the parent issue as the high-level goal; subtasks contain the detailed steps

Prefer subtasks over checklists in the body when items need to be tracked or assigned separately.

## During Implementation

Use **comments** to provide progress updates while working on an issue:

- Post a comment when starting work: summarize your approach or any decisions made
- Post updates when hitting blockers or changing direction
- Post a comment when opening a PR: include the PR link and a brief summary of what changed
- Keep comments factual and concise — they are a log of what happened, not a plan

**Do not update the task plan in the body once implementation starts.** The body captures the original scope; comments capture what actually happened.

## Assigning Issues

Always assign issues to the developer who will work on them:

- If you know the Linear user, assign directly
- If you only know their GitHub username, infer their identity — Linear and GitHub names are usually similar (e.g., GitHub `jsmith` → search for "jsmith" or "John Smith" in Linear)
- If working autonomously on behalf of a user, assign the issue to them
- Leave unassigned only if ownership is genuinely unclear

## Summary

| Situation        | Action                  |
| ---------------- | ----------------------- |
| New feature      | Create in **Backlog**   |
| New bug          | Create in **Triage**    |
| Scope & plan     | Write in **issue body** |
| Progress updates | Write in **comments**   |
| Complex work     | Use **subtasks**        |
| Ownership        | **Assign** to the dev   |
