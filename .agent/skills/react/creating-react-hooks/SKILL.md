---
name: creating-react-hooks
description: Generates Custom React Hooks for business logic orchestration and State Management.
---

# Creating React Hooks

## When to use this skill
- When a component needs data from an API.
- When orchestrating complex state (`useReducer`) or side effects.
- When reusing logic across components.

## Principles (Strict)
1.  **Orchestration**: Hooks bridge the gap between Components and API.
2.  **React Query v5**: MUST use `useQuery` or `useMutation` for server state.
3.  **Naming**: Must start with `use`.
4.  **Return Type**: Return explicit objects `{ data, actions, state }`.

## Workflow

### 1. Data Fetching Hook
Wrap the API module's query options.

```typescript
// hooks/useUserList.ts
import { useQuery } from '@tanstack/react-query';
import $api from '@/api';

export function useUserList() {
  const query = useQuery({
    ...$api.user.list(), // Returns QueryOptions
    staleTime: 1000 * 60, // 1 min
  });

  return {
    users: query.data ?? [],
    isLoading: query.isLoading,
    error: query.error,
    refetch: query.refetch
  };
}
```

### 2. Mutation Hook
Handle success/error flows (validations) here.

```typescript
// hooks/useUserActions.ts
import { useMutation, useQueryClient } from '@tanstack/react-query';
import $api from '@/api';

export function useUserActions() {
  const queryClient = useQueryClient();

  const createMutation = useMutation({
    mutationFn: $api.user.create,
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['users'] });
    }
  });

  return {
    createUser: createMutation.mutate,
    isCreating: createMutation.isPending
  };
}
```

## Checklist
- [ ] Does it use React Query for async data?
- [ ] Does it return a clean API for the component?
- [ ] Are conditional hooks avoided?
