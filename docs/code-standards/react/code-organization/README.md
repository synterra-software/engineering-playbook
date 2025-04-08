# Code Organization Standards

We support two architecture patterns depending on project requirements:

## 1. Component-First Architecture (Preferred)

```
ibex/
├── src/
│   ├── @components/                     # Shared React components
│   │   ├── Component/ 
│   │   │   ├── Component.tsx            # Component file
│   │   │   └── styled.ts                # Component styles
│   ├── constants/                       # Global constants
│   ├── extensions/                      # Third-party integrations
│   ├── gql/                             # GraphQL queries, mutations
│   ├── hooks/                           # Global hooks
│   ├── pages/                           # Pages with their specific components
│   │   ├── MainPage/
│   │   │   ├── components/              # Page-specific components
│   │   │   ├── hooks/                   # Page-specific hooks
│   │   │   ├── context/                 # Page-specific context
│   │   │   └── index.tsx                # Main page file
│   ├── providers/                       # Global contexts
│   ├── shared/                          # Shared business logic
│   └── utils/                           # Utility functions
```

**Benefits:**
- Clear separation between shared and page-specific components
- Components and related code are co-located
- Better for complex UI with many reusable components

## 2. Module-Based Architecture (Next.js)

```
app/
├── api/                       # API routes
├── (routes)/                  # Pages and routes
│   ├── dashboard/
│   │   └── page.tsx
│   └── settings/
│       └── page.tsx
├── _components/               # Shared components organized by module
│   ├── users/                 # User-related components
│   └── products/              # Product-related components
├── _hooks/                    # Shared hooks organized by module
│   ├── users/                 # User-related hooks
│   └── products/              # Product-related hooks
├── _store/                    # State management by module
│   ├── users/                 # User-related state
│   └── products/              # Product-related state
└── _utils/                    # Utility functions
```

**Benefits:**
- Organized by business domain/module instead of technical function
- Better isolation between features
- Easier to navigate related code across technical boundaries
- Ideal for Next.js projects with distinct business modules

## When to Use Each Architecture

**Component-First:** Use for traditional React SPAs with complex UI requirements

**Module-Based:** Use for Next.js projects with clear separation of business domains