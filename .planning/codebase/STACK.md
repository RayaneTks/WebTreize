# Tech Stack

## Core Technologies

- **Runtime**: Node.js (Next.js 16.1.6)
- **Language**: TypeScript 5.7.3
- **Framework**: Next.js 16.1.6 (App Router)
- **UI Library**: React 19.2.4

## Frontend

- **Styling**: Tailwind CSS 3.4.16
- **Animations**: Framer Motion 12.34.3
- **Icons**: Lucide React 0.575.0
- **Forms**: React Hook Form 7.71.2 + Zod 4.3.6
- **Class Utilities**: clsx 2.1.1, tailwind-merge 3.5.0, class-variance-authority 0.7.1

## Build & Dev

- **Package Manager**: npm (package-lock.json)
- **Bundler**: Next.js (built-in)
- **Linter**: ESLint 9.39.3 + eslint-config-next
- **PostCSS**: 8.4.49 (with Autoprefixer 10.4.20)
- **Image Optimization**: Sharp 0.34.5
- **Type Definitions**: @types/node 22.19.13, @types/react 19.2.14

## Fonts

- **Display**: Montserrat (700, 800, 900 weights)
- **Body**: Open Sans (400, 500, 600 weights)

## Colors

- Primary: Navy `#001F3F`
- Accent: Orange `#D9480F` (hover: `#B83E0D`)
- Background: Neutral `#F8F7F4`
- Text: Neutral `#6B7280`

## Configuration Files

- `next.config.ts` - Next.js configuration with security headers
- `tailwind.config.ts` - Custom theme with animations
- `tsconfig.json` - TypeScript configuration
- `.eslintrc.json` - ESLint (extends next/core-web-vitals)
- `postcss.config.mjs` - PostCSS with Tailwind

## Key Scripts

- `npm run dev` - Start development server
- `npm run build` - Production build
- `npm run start` - Start production server
- `npm run lint` - Run ESLint
