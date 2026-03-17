# Directory Structure

```
WebTreize/
├── app/                          # Next.js App Router
│   ├── api/
│   │   └── contact/
│   │       └── route.ts          # Contact form API endpoint
│   ├── legal/
│   │   ├── [slug]/
│   │   │   └── page.tsx          # Dynamic legal pages
│   │   └── layout.tsx            # Legal pages layout
│   ├── globals.css               # Global styles
│   ├── icon.svg                  # Site icon
│   ├── layout.tsx                # Root layout
│   ├── not-found.tsx             # 404 page
│   ├── page.tsx                  # Homepage
│   ├── robots.ts                 # Robots.txt
│   └── sitemap.ts                # Sitemap
│
├── components/
│   ├── ui/                       # Reusable UI primitives
│   │   ├── Badge.tsx
│   │   ├── Button.tsx            # CVA button variants
│   │   ├── Card.tsx
│   │   ├── FadeUp.tsx
│   │   ├── FaqItem.tsx
│   │   ├── LogoWebTreize.tsx
│   │   ├── SnapshatIcon.tsx
│   │   └── TechIconsPaths.ts
│   │
│   ├── sections/                 # Page sections
│   │   ├── CtaFinalSection.tsx
│   │   ├── ContactSection.tsx
│   │   ├── FaqSection.tsx
│   │   ├── GuaranteesSection.tsx
│   │   ├── HeroSection.tsx
│   │   ├── MethodologySection.tsx
│   │   ├── PainPointsSection.tsx
│   │   ├── ServicesSection.tsx
│   │   ├── SocialProofSection.tsx
│   │   └── VisionFaqSection.tsx
│   │
│   ├── background/
│   │   └── NoiseOverlay.tsx
│   │
│   ├── legal/
│   │   └── LegalWipContent.tsx
│   │
│   ├── ClientShell.tsx
│   ├── Footer.tsx
│   ├── MobileFab.tsx
│   └── Navbar.tsx
│
├── hooks/
│   └── useSmoothScroll.ts        # Smooth scroll hook
│
├── lib/
│   └── utils.ts                  # cn() utility (clsx + tailwind-merge)
│
├── public/                       # Static assets
│   ├── icon.svg
│   ├── logo.svg
│   ├── logo.png
│   ├── manifest.json
│   ├── og-image.jpg
│   └── snap.svg
│
├── .eslintrc.json
├── .gitignore
├── next.config.ts
├── package.json
├── package-lock.json
├── postcss.config.mjs
├── tailwind.config.ts
└── tsconfig.json
```

## Naming Conventions

- **Components**: PascalCase (e.g., `HeroSection.tsx`, `Button.tsx`)
- **Hooks**: camelCase with `use` prefix (e.g., `useSmoothScroll.ts`)
- **Utilities**: camelCase (e.g., `utils.ts`)
- **Files**: kebab-case for config files

## Organization Principles

1. **UI Components** - Small, reusable primitives (Button, Badge, Card)
2. **Section Components** - Large page sections (Hero, Services, Contact)
3. **Feature Components** - Domain-specific (Navbar, Footer)
4. **Layout Components** - Structural (ClientShell)
