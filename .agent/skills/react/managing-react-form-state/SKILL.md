---
name: managing-react-form-state
description: Manages complex form state using `useReducer` and custom hooks, avoiding giant `useState` objects.
---

# Managing React Form State

## When to use this skill
- When a form has more than 3 fields.
- When fields have inter-dependencies (e.g., "End Date must be after Start Date").
- When validation logic is complex.

## Principles (Strict)
1.  **useReducer**: Use `useReducer` for state transitions if multiple fields change together.
2.  **Custom Hook**: Encapsulate form logic (`useLoginForm`) separate from UI.
3.  **No Direct State**: Do not expose `setState` to the component; expose `handleXxx` handlers.
4.  **Validation**: Validation runs on change or submit, updating an `errors` object.

## Workflow

### 1. Define State & Actions
```typescript
interface FormState {
  email: string;
  age: number;
  errors: Record<string, string>;
}

type Action = 
  | { type: 'SET_EMAIL', payload: string }
  | { type: 'SET_AGE', payload: number }
  | { type: 'VALIDATE' };
```

### 2. Custom Hook
```typescript
export function useUserForm() {
  const [state, dispatch] = useReducer(reducer, initialState);

  const handleSubmit = () => {
    dispatch({ type: 'VALIDATE' });
    if (Object.keys(state.errors).length === 0) {
       // submit
    }
  };

  return { state, dispatch, handleSubmit };
}
```

## Checklist
- [ ] Is `useReducer` used for complex state?
- [ ] Is logic isolated in a custom hook?
- [ ] Are `errors` tracked in state?
