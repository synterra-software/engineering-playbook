# React Code Standards

## 1. Custom Hooks
* Minimize dependencies in useEffect, useMemo, and useCallback
* Avoid passing objects to hooks - pass primitive values when possible
* Understand the dependency array impact on re-renders

```tsx
// ✅ Good
const UserProfile = (userId: string) => {
  // Passing primitive value
  const user = useUser(userId);
  return <div>{user.name}</div>;
};

// ❌ Bad
const UserList = (options: { filter: string, sort: string }) => {
  // Passing object will cause re-renders even if content hasn't changed
  const users = useUsers(options);
  return <ul>{users.map(user => <li key={user.id}>{user.name}</li>)}</ul>;
};
```

## 2. Context for Dependency Injection
* Use Context API for dependency injection and state management
* Create contexts for features, not for individual values
* Avoid prop drilling by leveraging context

```tsx
// ✅ Good - Using context instead of prop drilling
const AuthContext = createContext<AuthContextType | null>(null);

export const useAuthContext = () => {
  const context = useContext(AuthContext);
  if (!context) throw new Error('useAuthContext must be used within AuthProvider');
  return context;
};
```

## 3. Memoization
* Use React.memo for components that render often
* Don't use memo for components that accept children as props
* Use useMemo for expensive calculations

```tsx
// ✅ Good - memoizing a component without children props
const UserList = React.memo(({ users }: { users: User[] }) => {
  return <ul>{users.map(user => <li key={user.id}>{user.name}</li>)}</ul>;
});

// ❌ Bad - unnecessary memoization with children props
const Container = React.memo(({ children }: { children: React.ReactNode }) => {
  return <div>{children}</div>;
});
```

## 4. State Management
* Use useState for simple component state
* Never use useReducer - use your project state management tool for complex state
* Understand when state should be local vs. global

## 5. Props
* Use FC and PropsWithChildren for typing components
* Destructure props in function parameters
* Provide default values when appropriate

```tsx
import { FC, PropsWithChildren } from 'react';

type ButtonProps = PropsWithChildren<{
  onClick: () => void;
  disabled?: boolean;
}>;

const Button: FC<ButtonProps> = ({ children, onClick, disabled = false }) => {
  return <button onClick={onClick} disabled={disabled}>{children}</button>;
};
```

## 6. Event Handlers
* Keep event handlers concise and focused
* Extract complex logic to separate functions

## 7. Single Responsibility
* Decouple logic from UI components
* Each component should focus on one responsibility
* Extract reusable logic into custom hooks

```tsx
// ✅ Good - Separation of concerns
const UserProfile = ({ userId }: { userId: string }) => {
  // Data fetching logic extracted to a hook
  const { user, loading, error } = useUser(userId);
  
  if (loading) return <Loader />;
  if (error) return <ErrorMessage error={error} />;
  
  // Component only handles rendering
  return <UserProfileView user={user} />;
};
```

## 8. Conditional Rendering
* Use ternary operators for simple conditions
* Extract complex conditional rendering to variables or functions

## 9. Component Structure
* Keep related files together in feature-based folders
* Follow a consistent file naming convention