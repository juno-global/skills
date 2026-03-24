# Open Pull Request

Prepare and open a pull request for the current feature branch.

## Steps

### 1. Verify Feature Branch

- Run `git branch --show-current` to get the current branch name
- If on `main`, create and switch to a feature branch (ask user for branch name or derive from context)
- Extract the Linear issue ID from the branch name (e.g., `jun-1234-feature-name` → `JUN-1234`) OR context

### 2. Commit All Changes

- Run `git status` to check for uncommitted changes
- Stage ALL changes including both modified files AND untracked files (use `git add -A`)
- Commit with a descriptive commit message. Follow the commit message format in our AGENTS.md.

### 3. Push Branch

- Push the branch to origin: `git push -u origin <branch-name>`

### 4. Analyze Changes for Linear Update

- Run `git diff main --stat` and `git diff main` to understand what changed
- Write a concise technical summary (3-5 bullet points) of the approach taken
- Add a comment to the Linear issue with this summary using an MCP tool
- **STOP** if you don't have access to a Linear MCP tool. Ask the user how they want to handle the Linear comment before proceeding.

### 5. Analyze Merge Checklist Readiness

Before creating the PR:

1. Read the Merge Checklist from `.github/PULL_REQUEST_TEMPLATE.md`
2. For each checklist item, analyze the diff to determine if it applies and if it can be checked
3. If any applicable items CANNOT be checked (e.g., missing auth checks, missing event emission):
   - STOP and present findings to user
   - Build a todo list of what needs to be fixed
   - Ask: "These items need to be addressed before opening the PR. Should I fix them now?"
   - If yes, fix the issues first, then return to this step

### 6. Create Pull Request

Once all applicable checklist items pass, generate the PR using `gh pr create`.

- Read `.github/PULL_REQUEST_TEMPLATE.md` for the exact format
- Fill in Summary, Quick Links (with correct JUN-XXXX), and Merge Checklist
- Pre-check items that were verified in step 5
- Remove checklist items that don't apply to this PR
- Do NOT deviate from the template format
- ALWAYS open the PR as a draft

### 7. Report

- Link to the created PR
- Reminder to add demo video if UI was changed
- List any checklist items that need manual verification
