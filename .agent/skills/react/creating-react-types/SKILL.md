---
name: creating-react-types
description: Generates strict TypeScript types/interfaces and Enums.
---

# Creating React Types

## When to use this skill
- When defining API responses.
- When defining Component props.
- When defining global application state shapes.

## Principles (Strict)
1.  **No Any**: Usage of `any` is strictly prohibited. Use `unknown` if absolutely necessary.
2.  **Interfaces > Types**: Prefer `interface` for object definitions.
3.  **Strict Null Checks**: Explicitly handle `null` vs `undefined`.
4.  **Enum Usage**: Use string enums for backend constants.

## Workflow

### 1. API Interface (Match DTO)
```typescript
// types/user.ts
export interface User {
  id: number;
  email: string;
  name: string;
  role: 'USER' | 'ADMIN'; // or Enum
  isActive: boolean;
  createdAt: string; // ISO Date String
}

export interface UserListResponse {
  content: User[];
  totalElements: number;
  totalPages: number;
}
```

### 2. Component Props
```typescript
interface UserCardProps {
  user: User;
  onEdit: (id: number) => void;
}
```

## Checklist
- [ ] Are all types exported?
- [ ] Is `any` completely absent?
- [ ] Do API types match Swagger/DTOs exactly?
