---
name: planning
description: Creates comprehensive implementation plans with bite-sized tasks. Use when requirements are clear but code has not started.
---

# Writing Plans

## When to use this skill
- When you have a spec or design but no code.
- Before writing any code for a multi-step task.
- To break down complex features into manageable steps.

## Workflow

### 1. Setup
- **Goal:** Write comprehensive implementation plans assuming the implementer has zero context.
- **Target:** `docs/plans/YYYY-MM-DD-<feature-name>.md`.

### 2. Plan Header
Every plan **MUST** start with this header:
```markdown
# [Feature Name] Implementation Plan

**Goal:** [One sentence describing what this builds]

**Architecture:** [2-3 sentences about approach]

**Tech Stack:** [Key technologies/libraries]

---
```

### 3. Task Granularity (Bite-Sized)
Break down work into tasks where each step is one action (2-5 minutes):
- "Write the failing test"
- "Run it to make sure it fails"
- "Implement the minimal code to make the test pass"
- "Run the tests and make sure they pass"
- "Commit"

### 4. Task Structure Template
```markdown
### Task N: [Component Name]

**Files:**
- Create: `exact/path/to/file.py`
- Modify: `exact/path/to/existing.py:123-145`

**Step 1: Write the failing test**
[Code Snippet]

**Step 2: Run test (Fail)**
Run: `pytest ...`

**Step 3: Write minimal implementation**
[Code Snippet]

**Step 4: Run test (Pass)**

**Step 5: Commit**
```

## Instructions

- **Exact file paths always**: Ambiguity leads to errors.
- **Complete code in plan**: Do not write "add validation", write the validation code.
- **Exact commands**: Include expected output where useful.
- **DRY, YAGNI, TDD**: Prioritize these principles in the plan.
