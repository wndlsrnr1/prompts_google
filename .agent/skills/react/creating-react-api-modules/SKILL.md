---
name: creating-react-api-modules
description: Generates Type-Safe API modules for React, returning QueryOptions for seamless React Query integration.
---

# Creating React API Modules

## When to use this skill
- When adding new endpoints to the frontend.
- When defining matching Typescript Interfaces for backend DTOs.

## Principles (Strict)
1.  **Functionality**: HTTP I/O only. No logic.
2.  **React Query Integration**: Fetcher functions should return `UseQueryOptions` where possible for read operations.
3.  **Typing**: All Promises must hold explicit Types. `Promise<UserDto>`.
4.  **Path**: `src/api/modules/*.ts`.

## Workflow

### 1. Define Types
Match the Backend DTOs strictly.

```typescript
export interface UserDto {
  id: number;
  email: string;
  name: string;
}

export interface CreateUserRequest {
  email: string;
  name: string;
}
```

### 2. Define Module
Group by domain.

```typescript
// src/api/modules/user.ts
import { UseQueryOptions } from '@tanstack/react-query';
import axios from '@/api/axiosInstance';
import { UserDto, CreateUserRequest } from '@/types/user';

const userApi = {
  // Query Factory Pattern
  list: (): UseQueryOptions<UserDto[]> => ({
    queryKey: ['users'],
    queryFn: async () => {
      const { data } = await axios.get<UserDto[]>('/api/v1/users');
      return data;
    }
  }),

  detail: (id: number): UseQueryOptions<UserDto> => ({
    queryKey: ['users', id],
    queryFn: async () => {
      const { data } = await axios.get<UserDto>(`/api/v1/users/${id}`);
      return data;
    },
    enabled: !!id
  }),

  // Mutation Function
  create: async (body: CreateUserRequest): Promise<UserDto> => {
    const { data } = await axios.post<UserDto>('/api/v1/users', body);
    return data;
  }
};

export default userApi;
```

## Checklist
- [ ] Are keys defined as snake_case if backend requires it? (Or mapped via interceptor)
- [ ] Do Read methods return objects with `queryKey` and `queryFn`?
- [ ] Are Types exported?
