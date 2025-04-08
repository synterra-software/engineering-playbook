# TypeScript Code Standards

## 1. No `any` Type
* Avoid using `any` type unless absolutely necessary
* If needed, add a comment explaining why

```typescript
// ✅ Good
function processData(data: unknown): void {
    if (typeof data === 'string') {
        // Type-safe operation
    }
}

// ❌ Bad
function processData(data: any): void {
    // Unsafe operations
}
```

## 2. Enums Over Union Types
* Use enums instead of string literal unions

```typescript
// ✅ Good
enum UserRole {
    Admin = 'admin',
    Editor = 'editor',
    Viewer = 'viewer'
}

// ❌ Bad
type UserRole = 'admin' | 'editor' | 'viewer';
```

## 3. Strong Typing
* Always define parameter and return types for functions

```typescript
// ✅ Good
function getUsers(): Promise<User[]> {
    // implementation
}

// ❌ Bad
function getUsers() {
    // Return type is implicit
}
```

## 4. Naming Conventions
* Use `PascalCase` for types, interfaces, classes, and enums
* Use `camelCase` for variables, functions, and properties
* Use `UPPER_SNAKE_CASE` for constants

## 5. Error Handling
* Never ignore caught errors
* Provide meaningful error messages

## 6. Use `const` by Default
* Use `const` for variables that don't need to be reassigned
* Use `let` only when necessary
* Never use `var`

## 7. Optional Chaining
* Use optional chaining (`?.`) and nullish coalescing (`??`)

```typescript
// ✅ Good
const name = user?.profile?.name ?? 'Guest';

// ❌ Bad
const name = user && user.profile && user.profile.name ? user.profile.name : 'Guest';
```

## 8. Strict Mode
* Enable `strict: true` in tsconfig.json

## 9. Type Exports
* Export reusable types from dedicated files
* Use explicit imports, not wildcard imports