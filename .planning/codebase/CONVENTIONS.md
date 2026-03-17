# Code Conventions

## Language

- **TypeScript** - Strict mode enabled
- **React 19** with functional components
- **Next.js 16** App Router

## Component Patterns

### File Structure
```typescript
import * as React from "react"
import { cn } from "@/lib/utils"

export function ComponentName() {
  return (/* JSX */)
}
```

### Client Components
Mark with `'use client'` directive for:
- Event handlers (onClick, onChange)
- useState, useEffect
- Framer Motion animations
- Custom hooks

### Props Interface
```typescript
export interface ComponentProps extends React.HTMLAttributes<HTMLElement> {
  variant?: 'default' | 'secondary' | 'outline'
  size?: 'default' | 'sm' | 'lg'
}
```

## Styling

- **Tailwind CSS** for all styling
- **Custom theme** in `tailwind.config.ts`
- **CVA (class-variance-authority)** for variant components
- **cn() utility** merges classes: `cn(baseClass, variantClasses, className)`

## CSS Patterns

- Responsive: `md:`, `lg:` prefixes
- Dark mode: `dark:` prefix (configured via class)
- Custom animations defined in tailwind.config.ts
- Color palette: `navy`, `orange`, `neutral-bg`, `neutral-text`

## Component Categories

1. **UI Primitives** (`components/ui/`) - Buttons, badges, cards
2. **Sections** (`components/sections/`) - Full page sections
3. **Layout** - Navbar, Footer, ClientShell

## Imports

- Use `@/` path alias for imports
- Order: React → external → internal (grouped)

## Error Handling

- Form validation with Zod schemas
- API routes return structured error responses
- Console logging for errors in API routes

## TypeScript

- Strict mode enabled
- Avoid `any` type
- Use proper types from React, Next.js

## Naming

- PascalCase: Components, interfaces, types
- camelCase: Variables, functions, files
- camelCase with `use` prefix: Custom hooks
