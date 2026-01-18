# Design: Generating Workflows Skill

## Overview
A new skill `generating-workflows` that enables the agent to create valid Antigravity workflow files (`.md`) from natural language user requests.

## Goals
- **Natural Language Interface**: Users can say "Make a workflow to test and deploy" without knowing the file format.
- **Accuracy**: Generated workflows must reference *existing* skills and valid commands.
- **Safety**: Generated workflows should include necessary checks (e.g., git status) by default.

## Skill Structure (`.agent/skills/generating-workflows/SKILL.md`)

The skill will guide the agent through these steps:

1.  **Analyze Request**: Identify the goal (e.g., "Daily Clean Up", "Release Process").
2.  **Scan Capabilities**: List available skills in `.agent/skills` to know what building blocks are available.
3.  **Draft Workflow**:
    -   Define YAML frontmatter (description).
    -   Create steps mapping to existing skills.
    -   Add `// turbo` annotations for safe automated commands.
4.  **Validate**: Ensure all referenced paths exist.
5.  **Save**: Write to `.agent/workflows/{kebab-case-name}.md`.

## Output Metadata
- **Location**: `.agent/workflows/`
- **Naming Convention**: `verb-noun.md` (e.g., `deploy-app.md`, `run-tests.md`)

## Example Interaction
User: "매일 아침 상태 점검하고 브랜치 업데이트하는 워크플로우 만들어줘"
Agent: (Uses skill) -> Creates `.agent/workflows/daily-morning-routine.md`
