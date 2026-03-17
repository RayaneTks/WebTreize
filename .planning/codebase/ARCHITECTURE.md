# Architecture

## Pattern

- **Next.js App Router** with Server Components by default
- Client Components marked with `'use client'` directive
- API Routes in `app/api/` directory

## Rendering Strategy

- **Server Components**: Default for pages and layouts
- **Client Components**: Interactive elements (animations, forms, scroll handling)
- **Static Generation**: Pages pre-rendered at build time
- **Dynamic API**: Contact form endpoint (`app/api/contact/route.ts`)

## Data Flow

```
User Request → Next.js Router → Server Components → API Routes → External Services
                                  ↓
                            Client Components (hydration)
```

## Key Abstractions

- **UI Components**: Reusable primitives in `components/ui/`
- **Section Components**: Page sections in `components/sections/`
- **Utilities**: Shared functions in `lib/utils.ts`
- **Hooks**: Custom hooks in `hooks/`

## Entry Points

- **Pages**: `app/page.tsx` (main), `app/legal/[slug]/page.tsx` (dynamic)
- **API**: `app/api/contact/route.ts` (POST)
- **Layouts**: `app/layout.tsx` (root), `app/legal/layout.tsx` (legal pages)

## Security

- Content Security Policy headers configured
- X-Frame-Options: DENY
- Strict-Transport-Security enabled
- Referrer-Policy: strict-origin-when-cross-origin

## State Management

- React Hook Form for form state
- URL-based state (Next.js routing)
- No global state library (simple app requirements)

## Performance Optimizations

- Font optimization via `next/font`
- Image optimization with configured device sizes
- CSS caching via custom headers
- Client-side motion with Framer Motion
