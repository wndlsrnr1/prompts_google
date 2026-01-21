---
name: creating-react-utils
description: Generates pure utility functions for formatting, validation, and data transformation.
---

# Creating React Utils

## When to use this skill
- When formatting dates, numbers, or currency.
- When transforming data structures (e.g., array to map).
- When validating regex patterns.

## Principles (Strict)
1.  **Pure Functions**: No side effects. Output depends ONLY on input.
2.  **Date-fns**: Use `date-fns` for date manipulation.
3.  **Strict Typing**: Arguments and return types must be explicit.
4.  **Unit Tests**: Utils are the easiest to test; encourage testing.

## Workflow

### 1. Date Formatter
```typescript
import { format } from 'date-fns';

export function formatDate(dateStr: string): string {
  if (!dateStr) return '';
  return format(new Date(dateStr), 'yyyy.MM.dd HH:mm');
}
```

### 2. Data Transformer
```typescript
export function toMap<T extends { id: number }>(list: T[]): Record<number, T> {
  return list.reduce((acc, item) => {
    acc[item.id] = item;
    return acc;
  }, {} as Record<number, T>);
}
```

## Checklist
- [ ] Is it a pure function?
- [ ] Are types strict?
- [ ] Are side effects (API calls, DOM access) avoided?
