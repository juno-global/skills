# Juno Skills & Commands

Curated agent skills and commands for [Tron](https://github.com/juno-global/tron) sandboxes. Add this repo as a skill source in Tron to make everything here available in your sandboxes.

## Quick Start

1. Go to **Settings → Team → Skill Sources** in Tron
2. Add `juno-global/skills` as a source
3. All skills and commands in this repo will auto-install in every new sandbox

## Repository Structure

This repo follows the [Vercel Skills convention](https://github.com/vercel-labs/skills):

```
skills/
├── <skill-name>/
│   ├── SKILL.md          # Required — the skill definition
│   ├── scripts/           # Optional — helper scripts the skill references
│   └── references/        # Optional — reference docs or examples
commands/
├── <command-name>.md      # A slash command
└── <namespace>/           # Optional — group related commands
    └── <command-name>.md
```

- **Skills** go in `skills/<name>/SKILL.md` (each skill gets its own directory)
- **Commands** go in `commands/<name>.md` (flat files, with optional subfolder namespacing)

---

## Skills vs Commands — When to Use Which

| | Skill | Command |
|---|---|---|
| **What it is** | Persistent knowledge the agent loads when relevant | A step-by-step workflow triggered by a slash command |
| **How it activates** | Automatically — the agent loads it based on the `description` field | Manually — the user types `/<command-name>` |
| **Best for** | Conventions, best practices, style guides, domain knowledge, tool usage patterns | Multi-step workflows, runbooks, deployment procedures, repetitive tasks |
| **Examples** | "Always use Tailwind classes instead of inline styles", "Follow our PR naming convention" | `/ship/open-pr` — commit, push, create PR; `/ship/fix-tests` — run tests and fix failures |
| **Analogy** | A reference guide the agent consults | A checklist the agent executes |

**Rule of thumb:** If the agent should _always know_ something → **skill**. If the agent should _do_ something on demand → **command**.

---

## Contributing

There are two ways to contribute: **via the agent** (recommended for non-technical users) or **manually via PR**.

### Option 1: Via the Agent (Recommended)

If you're in a Tron sandbox with `juno-global/skills` configured as a skill source, the agent can create and contribute skills for you:

1. **Describe what you want:**
   > "I want a skill that enforces our API error handling conventions"

2. **The agent creates it** — writes the SKILL.md, tests it in your sandbox immediately

3. **Tell the agent to share it:**
   > "Save this to the team skills repo"

4. **The agent opens a PR** — creates a branch on `juno-global/skills`, commits the skill, and opens a pull request

5. **A teammate reviews and merges** — the skill auto-installs in all future sandboxes

You never need to write markdown or use git. The agent handles everything.

### Option 2: Manual PR

1. Fork or clone this repo
2. Create a branch: `git checkout -b add-<skill-name>`
3. Add your skill or command (see format guides below)
4. Commit and push
5. Open a PR with a description of what the skill/command does and when it should be used

---

## Skill Format

Each skill lives in its own directory under `skills/`.

### Required: `skills/<name>/SKILL.md`

```markdown
---
name: <name>
description: <1-2 sentences — when should the agent load this skill?>
---

# <Title>

<Detailed instructions for the agent>
```

### Frontmatter Fields

| Field | Required | Description |
|---|---|---|
| `name` | Yes | Lowercase, hyphenated identifier (e.g., `react-best-practices`). Must match the directory name. |
| `description` | Yes | 1-2 sentences describing **when** the agent should load this skill. This is the trigger — be specific. |

The `description` is critical — it's what the agent uses to decide whether to load the skill for a given task. Good descriptions are specific and action-oriented:

- ✅ `"React component patterns and performance best practices. Use when writing new React components or reviewing React code."`
- ✅ `"API error handling conventions for Hono backends. Use when creating API routes or handling errors."`
- ❌ `"React stuff"` (too vague — agent won't know when to load it)
- ❌ `"Useful tips"` (not actionable)

### Body Content Guidelines

- **Write for the agent, not a human reader.** Use imperative language: "Always use...", "Never commit...", "Check for..."
- **Be concrete.** Code examples and specific patterns are more useful than abstract principles.
- **Keep it focused.** One skill per concern. Don't mix "React patterns" with "database conventions."
- **Use headers to organize.** The agent can scan headings to find relevant sections quickly.
- **Include examples.** Show the right way (and optionally the wrong way) with code blocks.

### Optional: Supporting Files

Skills can include helper scripts and reference docs alongside the SKILL.md:

```
skills/deploy-to-prod/
├── SKILL.md              # The skill definition
├── scripts/
│   └── pre-deploy.sh     # Script the skill references
└── references/
    └── runbook.md        # Additional context
```

These files are uploaded alongside the SKILL.md when installed. Reference them in your skill with relative paths.

---

## Command Format

Commands are single `.md` files under `commands/`.

### `commands/<name>.md` or `commands/<namespace>/<name>.md`

```markdown
# <Command Title>

<Brief description of what this command does — 1-2 sentences.>

## Overview

<Optional — more context about when and why to use this command.>

## Steps

1. **Step name** — detailed instructions for this step
2. **Step name** — detailed instructions for this step
3. **Step name** — detailed instructions for this step
```

### Command naming

- The filename becomes the slash command: `deploy.md` → `/deploy`
- Use subfolder namespacing for related commands: `ship/open-pr.md` → `/ship/open-pr`
- Use lowercase, hyphenated names: `fix-tests.md`, not `FixTests.md`

### Frontmatter (Optional for Commands)

Commands **do not require YAML frontmatter**. The `# Title` heading and first paragraph serve as the name and description. However, you may optionally include frontmatter for consistency:

```markdown
---
name: deploy
description: Run the full deployment pipeline for the current branch.
---

# Deploy to Production
...
```

### Body Content Guidelines

- **Structure as numbered steps.** The agent executes them sequentially.
- **Bold the step names.** Makes it easy to scan: `1. **Run checks** — Execute...`
- **Be explicit about commands.** Include the actual shell commands, file paths, and expected outputs.
- **Handle failure cases.** Tell the agent what to do if a step fails.
- **End with a report step.** Have the agent summarize what happened and link to artifacts (PRs, deploys, etc.).

---

## Quality Checklist

Before submitting a PR, verify:

- [ ] Skill directory name matches the `name` field in frontmatter
- [ ] `description` field clearly states when the skill should activate
- [ ] Content is written for the agent (imperative, concrete, with examples)
- [ ] No sensitive data (API keys, internal URLs, credentials)
- [ ] Tested in a sandbox — the skill/command works as expected
- [ ] Focused on a single concern (not a grab-bag of unrelated topics)

---

## Examples

### Skill Example

See [`skills/`](./skills/) for live examples (when available).

Minimal skill:

```markdown
---
name: commit-conventions
description: Git commit message conventions. Use when creating commits or reviewing commit history.
---

# Commit Conventions

Always use conventional commit format: `type(scope): description`

**Types:** feat, fix, refactor, docs, test, chore, ci

**Rules:**
- Keep the subject line under 72 characters
- Use imperative mood: "Add feature" not "Added feature"
- Reference issue IDs: `feat(auth): add SSO login (JUN-1234)`
```

### Command Example

See [`commands/ship/`](./commands/ship/) for live examples.

---

## License

MIT
