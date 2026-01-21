---
name: managing-react-global-state
description: Manages global client-side state using Redux Toolkit or Context, STRICTLY separating server state (React Query) from client state.
---

# Managing React Global State

## When to use this skill
- When state is truly global (Theme, Auth User, Sidebar status).
- **NEVER** for API data (Use React Query).

## Principles (Strict)
1.  **Client State Only**: Only store UI state (modals, themes) or Session state (token, user info).
2.  **Slices**: Use Redux Toolkit `createSlice` for modularity.
3.  **Selectors**: Access state ONLY via selectors (`selectTheme`), never raw state.
4.  **Immutability**: Redux Toolkit handles this, but be aware.

## Workflow

### 1. Define Slice
```typescript
const authSlice = createSlice({
  name: 'auth',
  initialState,
  reducers: {
    setCredentials: (state, action) => {
      state.user = action.payload;
      state.token = action.payload.token;
    },
    logout: (state) => {
      state.user = null;
      state.token = null;
    }
  }
});
```

### 2. Store Config
```typescript
export const store = configureStore({
  reducer: {
    auth: authSlice.reducer
  }
});
```

## Checklist
- [ ] Is Server State (API data) EXCLUDED from this store?
- [ ] Are Selectors used?
- [ ] Is the state truly global?
