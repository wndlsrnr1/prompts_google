---
name: creating-react-components
description: Generates React Function Components focusing on rendering only. Enforces strict separation from logic (Hooks).
---

# Creating React Components

## When to use this skill
- When building UI pages or widgets.
- When breaking down a large view into sub-components.

## Principles (Strict)
1.  **Render Only**: Components must NOT contain business logic or async headers.
2.  **No Direct API**: NEVER call `fetch`, `axios`, or `useQuery` directly in the component. Call a custom hook instead.
3.  **Strict PropTypes**: Always define `interface Props`.
4.  **Mobile First**: Use Tailwind CSS with mobile breakpoints (`w-full`, `p-4`).

## Workflow

### 1. Define Props
Expose event handlers for interactions.

```typescript
interface UserListProps {
  users: User[];
  onSelect: (id: string) => void;
}
```

### 2. Connect Hook (Container/View pattern)
If it's a page component, connect the hook. If it's a presentational component, receive props.

```typescript
// components/UserListContainer.tsx
import { useUserList } from '@/hooks/useUserList';

export default function UserListContainer() {
  const { data: users, isLoading, error } = useUserList(); // Hook handles logic

  if (isLoading) return <Spinner />;
  if (error) return <ErrorBanner message={error.message} />;

  return <UserListView users={users} onSelect={console.log} />;
}
```

### 3. Implementation (View)
Focus on JSX and Tailwind classes.

```typescript
// components/UserListView.tsx
export default function UserListView({ users, onSelect }: UserListProps) {
  return (
    <ul className="divide-y divide-gray-200">
      {users.map(user => (
        <li 
          key={user.id} 
          onClick={() => onSelect(user.id)}
          className="p-4 hover:bg-gray-50 active:bg-gray-100 cursor-pointer"
        >
          <span className="font-medium text-gray-900">{user.name}</span>
        </li>
      ))}
    </ul>
  );
}
```

## Checklist
- [ ] Are API calls completely absent?
- [ ] Is `useEffect` absent? (Data fetching must stand in hooks)
- [ ] Are props typed with an Interface?
- [ ] Is Tailwind used for styling?
