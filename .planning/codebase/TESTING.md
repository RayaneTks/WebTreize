# Testing

## Current State

- **No test framework configured**
- No tests currently exist in the codebase

## Recommendations

### Immediate

- Install Vitest or Jest + React Testing Library
- Add `@testing-library/react`, `@testing-library/jest-dom`
- Add `vitest` or `jest` scripts to package.json

### Testing Strategy

1. **Unit Tests** (`lib/utils.ts`, components)
2. **Component Tests** - Render and interaction tests
3. **Integration Tests** - API routes, form submissions

### Suggested Setup (Vitest)

```bash
npm install -D vitest @testing-library/react @testing-library/jest-dom jsdom
```

```typescript
// vitest.config.ts
import { defineConfig } from 'vitest/config'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  test: {
    environment: 'jsdom',
    globals: true,
    setupFiles: ['./test/setup.ts'],
  },
})
```

### Test Structure

```
test/
├── setup.ts
├── utils.test.ts
├── components/
│   └── Button.test.tsx
└── integration/
    └── contact.test.ts
```

### Priority Files to Test

1. `lib/utils.ts` - cn() function
2. `components/ui/Button.tsx` - CVA variants
3. `app/api/contact/route.ts` - Form validation
4. Section components - Render tests

## Linting

- ESLint configured with `next/core-web-vitals`
- Run: `npm run lint`
