# Concerns & Technical Debt

## High Priority

### Production Readiness

1. **Resend API not configured**
   - Location: `app/api/contact/route.ts:3-7`
   - Issue: API key placeholder, needs real configuration before launch
   - Impact: Contact form logs to console instead of sending emails

2. **Placeholder phone number**
   - Location: `app/layout.tsx:70`
   - Issue: `'+33 4 00 00 00 00'` is placeholder
   - Impact: SEO, schema.org listing incorrect

### Missing Tests

- No test framework configured
- No test files exist
- Risk: Regression issues with refactoring

## Medium Priority

### Code Quality

3. **Magic numbers in animations**
   - Location: `components/sections/HeroSection.tsx`
   - Issue: Hardcoded delay/duration values (0.6, 0.8, 1, etc.)
   - Recommendation: Extract to constants

4. **Type `as any` usage**
   - Location: `components/sections/HeroSection.tsx:28`
   - Issue: `ease: [0.16, 1, 0.3, 1] as any`
   - Should use proper cubic-bezier type

### SEO & Content

5. **Hardcoded content**
   - All content in components
   - Recommendation: Consider CMS or content layer for maintainability

6. **Legal pages placeholder**
   - Location: `app/legal/[slug]/page.tsx`
   - Issue: Returns "Work in progress" message

## Low Priority

### Developer Experience

7. **No dev scripts for testing**
   - Only `dev`, `build`, `start`, `lint`
   - Could add `test`, `typecheck`

8. **Environment variables not documented**
   - No `.env.example` file

### Performance

9. **Large HeroSection component**
   - 200+ lines, multiple motion elements
   - Consider splitting into smaller components

10. **No image optimization**
    - Using static images in public folder
    - Could benefit from next/image with remote patterns

## Security

- CSP configured properly in next.config.ts
- No sensitive data in codebase
- API routes have input validation with Zod

## Accessibility

- Good: Skip-to-content link in layout
- Good: ARIA labels on interactive elements
- Could add: More comprehensive a11y testing

## Future Enhancements

- Add analytics tracking
- Implement A/B testing
- Add internationalization (i18n)
- Consider CMS integration for content
