---
description: High-Definition workflow for React features. Enforces strict separation: Types -> API -> Logic (Hooks) -> UI (Components).
---

# React Feature Development Workflow (Smart)

This workflow ensures strict separation of concerns from Data to UI.

## 1. Type Definitions
**Goal**: clear contract with backend.
- **Skill**: `view_file .agent/skills/react/creating-react-types/SKILL.md`
- **Action**: Create interfaces in `src/types/`. Match Backend DTOs exactly.

## 2. API Integration
**Goal**: Define network requests.
- **Skill**: `view_file .agent/skills/react/creating-react-api-modules/SKILL.md`
- **Skill**: `view_file .agent/skills/react/creating-react-utils/SKILL.md` (If formatters needed)
- **Action**: Create API function returning `Promise<Dto>`.

## 3. Business Logic (Hooks)
**Goal**: State management and Data orchestration.
- **Skill**: `view_file .agent/skills/react/creating-react-hooks/SKILL.md`
- **Skill**: `view_file .agent/skills/react/managing-react-form-state/SKILL.md` (If complex form)
- **Action**: Create `useXxx` hook. Use `useQuery`/`useMutation`. Return handlers.

## 4. UI Implementation (Visuals)
**Goal**: Render the view.
- **Skill**: `view_file .agent/skills/react/creating-react-components/SKILL.md`
- **Action**: Create `.tsx` file. Connect to the Hook.
- **Constraint**: NO logic in JSX. Only `map`, `filter`, and binding.

## 5. Global State (Optional)
**Goal**: Client-side global settings.
- **Skill**: `view_file .agent/skills/react/managing-react-global-state/SKILL.md`
- **Action**: Only update if feature requires global theme/auth changes.
