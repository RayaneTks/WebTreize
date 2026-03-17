# External Integrations

## Email Service (Resend)

- **API**: Resend (`https://api.resend.com/emails`)
- **Purpose**: Contact form email delivery
- **Environment Variables**:
  - `RESEND_API_KEY` - API key for Resend
  - `NEXT_PUBLIC_CONTACT_EMAIL` or `CONTACT_EMAIL` - Destination email (default: `contact@webtreize.com`)
- **Status**: TODO before production deployment (see `app/api/contact/route.ts:3-7`)
- **Fallback**: Logs lead info to console if API key not configured

## Fonts

- **Google Fonts**: Montserrat, Open Sans (loaded via `next/font/google`)

## SEO & Meta

- **Schema.org**: Organization, LocalBusiness, FAQPage (JSON-LD in `app/layout.tsx`)
- **Sitemap**: Auto-generated via `app/sitemap.ts`
- **Robots**: Configured via `app/robots.ts`

## Analytics (Implied)

- No analytics SDK currently integrated
- Placeholder for future tracking integration

## Environment Variables

| Variable | Required | Purpose |
|----------|----------|---------|
| `NEXT_PUBLIC_SITE_URL` | No | Site URL (default: `https://www.webtreize.com`) |
| `RESEND_API_KEY` | No* | Email delivery (*optional - falls back to console log) |
| `NEXT_PUBLIC_CONTACT_EMAIL` | No | Contact form destination |
| `CONTACT_EMAIL` | No | Fallback contact destination |

## Future Integrations (TODO)

- Resend configuration for production
- Analytics platform (Google Analytics, Plausible, etc.)
- Form submission webhook for CRM
