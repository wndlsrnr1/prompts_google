---
name: configuring-persona
description: Dynamically loads persona definitions, instructions, and styles from the global prompt armory (`.agent/prompts`). Use to switch the agent's role or enforce specific behavior patterns for the current session.
---

# Configuring Persona (Dynamic Injection)

## When to use this skill
- When the user asks to "act as X" or "switch mode to Y".
- When a task requires a specific specialized mindset (e.g., Security Auditor, Technical Writer).
- When the user wants to enforce a specific output format or style globally for the session.

## Workflow
1.  **Identify Components**: Determine which `persona`, `instruction`, and `style` modules are needed.
2.  **Locate Modules**: Check `.agent/prompts/` for the corresponding markdown files.
3.  **Inject Context**: Read the content of the selected modules.
4.  **Activate Mode**: Declare the new persona and apply its rules to all subsequent responses.

## Instructions
- Use `view_file` to read the module contents.
- Combined the content into a single mental context block:
  ```markdown
  <ACTIVE_PERSONA>
  [Role Definition from personas/*.md]
  [Specific Instructions from instructions/*.md]
  [Style Guide from styles/*.md]
  </ACTIVE_PERSONA>
  ```
- Acknowledge the mode switch to the user: "Activated **[Persona Name]** mode with **[Style]** style."

## Available Modules (Check dir for full list)
- **Personas**: `strict-reviewer`, `creative-writer`, `teacher`...
- **Instructions**: `json-output`, `ddd-style`, `korean-only`...
- **Styles**: `concise`, `detailed`...
