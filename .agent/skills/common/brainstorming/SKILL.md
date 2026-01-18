---
name: brainstorming
description: Explores user intent, requirements, and design before implementation. Use before creative work or when requirements are ambigous.
---

# Brainstorming Ideas Into Designs

## When to use this skill
- Before starting any creative work (creating features, building components).
- When requirements are vague or ambiguous.
- To refine ideas into specific designs.

## Workflow

### 1. Understand the idea
- **Context:** Check out the current project state first (files, docs, recent commits).
- **Inquiry:** Ask questions *one at a time* to refine the idea.
- **Format:** Prefer multiple choice questions when possible.
- **Focus:** Understanding purpose, constraints, and success criteria.

### 2. Explore approaches
- Propose 2-3 different approaches specifically identifying trade-offs.
- Lead with your recommended option and explain why.

### 3. Present the design
- Once you believe you understand what you're building, present the design.
- **Incremental:** Break it into sections of 200-300 words.
- **Validation:** Ask after each section whether it looks right so far.
- **Coverage:** Architecture, components, data flow, error handling, testing.

### 4. Documentation
- Write the validated design to `docs/plans/YYYY-MM-DD-<topic>-design.md`.

## Instructions

- **One question at a time**: Don't overwhelm the user.
- **YAGNI ruthlessly**: Remove unnecessary features from all designs.
- **Incremental validation**: detailed feedback is easier on small chunks.
- **Be flexible**: Go back and clarify when something doesn't make sense.
