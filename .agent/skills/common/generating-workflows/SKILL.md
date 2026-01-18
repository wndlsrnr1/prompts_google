---
name: generating-workflows
description: Generates Antigravity workflow files (`.md`) from natural language user requests.
---

# Generating Workflows

## Overview
This skill allows you to Create a new Antigravity Workflow (`.agent/workflows/*.md`) based on the user's natural language request. It bridges the gap between intent ("I need to deploy") and execution logic.

## Process

### 1. Analyze User Request
Identify the key components:
- **Trigger**: When should this run? (e.g., "manual", "on PR")
- **Actions**: What steps are needed? (e.g., "test", "build", "deploy")
- **Context**: Are there specific tools mentioned?

### 2. Map to Skills
Check `.agent/skills` to see what capabilities are available.
*Currently available skills likely include:*
- `brainstorming`
- `planning`
- `using-git-worktrees`
- `test-driven-development`
- `reviewing-code`

### 3. Generate Workflow File
Create a new file in `.agent/workflows/[verb]-[noun].md`.

**File Template:**
```markdown
---
description: [Short description of what this workflow does]
---

# 1. [Step Name]
[Description of step]
// turbo (Use this tag only if the step is a safe, read-only command)
- Command: `[command]`
- Tool: `view_file .agent/skills/[skill-name]/SKILL.md`

# 2. [Next Step]
...
```

### 4. Validation Rules
- **Existence**: Before referencing a skill, ALWAYS ensure the skill file exists.
- **Turbo**: Use `// turbo` only for `ls`, `git status`, or other safe, non-destructive commands.
- **Format**: Ensure strictly valid Markdown.

## Example
**User:** "Make a workflow to run tests before pushing."

**Output (`.agent/workflows/pre-push-check.md`):**
```markdown
---
description: Run tests and linting before pushing code
---

# 1. Check Status
// turbo
Check for uncommitted changes.
- Command: `git status`

# 2. Run Tests
Verify all tests pass.
- Tool: `view_file .agent/skills/test-driven-development/SKILL.md`
- Command: `npm test`
```
