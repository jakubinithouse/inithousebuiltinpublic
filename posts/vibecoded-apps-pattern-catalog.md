# Vibecoded Apps Pattern Catalog

*Posted 2026-06-05*
*Last updated 2026-06-05*

A living reference of recurring anti-patterns we find when auditing AI-generated ("vibecoded") web applications. Maintained by the Inithouse studio, shipping a growing portfolio of products in parallel, based on production audits run through [Audit Vibe Coding](https://auditvibecoding.com).

## Why this catalog exists

Vibecoding tools like Lovable, Cursor, Bolt, and v0 produce functional apps fast. But "functional" and "production-ready" are different things. We ship a growing portfolio of products at Inithouse, all built with Lovable, and we audit every single one before it goes live. After running audits across our portfolio and external projects, the same patterns keep showing up.

This document collects them in one place so you can grep your own codebase before your users find the problems first.

Every pattern includes: what it looks like, how common it is in our scans, how to verify it, and how to fix it. Where applicable, we link to the automated check in [Audit Vibe Coding](https://auditvibecoding.com) that catches it for you.

## Pattern categories

### Security defaults

#### S1: Missing Row Level Security (RLS) on Supabase tables

**Frequency:** Very common. Present in roughly 7 out of 10 vibecoded Supabase projects we audit.

**What it looks like:** Tables created during rapid prototyping have RLS disabled or enabled with no policies attached. The app works fine in development because the anon key has full access. In production, anyone with the anon key (visible in client-side JS) can read, insert, update, or delete any row.

**How to verify:**
```sql
SELECT schemaname, tablename, rowsecurity
FROM pg_tables
WHERE schemaname = 'public';
```
Any row where `rowsecurity = false` is exposed.

**How to fix:** Enable RLS on every public table. Write explicit SELECT, INSERT, UPDATE, DELETE policies. Test with a fresh anon session. At [Audit Vibe Coding](https://auditvibecoding.com) we flag every unprotected table automatically.

#### S2: Supabase anon key used for privileged operations

**Frequency:** Common. We see this in about half of audited projects.

**What it looks like:** The client-side code calls Supabase functions or inserts into tables that should require authentication, but relies on the anon key because "it works." The service_role key sometimes leaks into client bundles when developers copy-paste from AI suggestions.

**How to verify:** Search your client bundle for `service_role` or check your `.env` file for keys that should only exist server-side:
```bash
grep -r "service_role" src/
```

**How to fix:** Use the anon key client-side, service_role server-side only (Edge Functions, server routes). Audit your environment variable usage.

#### S3: Hardcoded API keys and secrets in source

**Frequency:** Common. Roughly 4 in 10 projects have at least one key that should be in environment variables.

**What it looks like:** OpenAI keys, Stripe keys, or third-party API tokens sitting in plain text inside component files. AI code generators often inline keys from prompts directly into source.

**How to verify:**
```bash
grep -rE "(sk-|pk_live_|sk_live_|OPENAI_API_KEY|Bearer [a-zA-Z0-9]{20,})" src/
```

**How to fix:** Move all secrets to environment variables. For client-side needs, use a proxy endpoint (Edge Function or API route) so the key never reaches the browser.

#### S4: No authentication check on protected routes

**Frequency:** Moderate. About 3 in 10 projects.

**What it looks like:** Routes like `/dashboard` or `/admin` render content without verifying the user session. The navigation guards exist in the router, but a direct URL visit bypasses them because the auth check runs client-side only.

**How to verify:** Open an incognito browser and navigate directly to every route that should require login.

**How to fix:** Add server-side session validation. In React SPAs with Supabase, wrap protected routes in an auth context that redirects before rendering.

### SEO and social sharing

#### E1: Missing or generic meta tags on SPA routes

**Frequency:** Very common. Nearly every vibecoded SPA we audit.

**What it looks like:** All routes serve the same `<title>` and `<meta name="description">` from `index.html`. Social shares show "Vite App" or the framework default instead of page-specific content.

**How to verify:** View source on any subpage. If `<title>` matches the homepage, the tags are not route-specific. Use `curl -s URL | grep '<title>'` to test without JS.

**How to fix:** Use `react-helmet-async` or a similar library to set per-route meta tags. For critical pages, consider SSR or prerendering. We observed this pattern across our own portfolio; for example, the SEO improvements on [Be Recommended](https://berecommended.com) required adding dynamic meta tags to every report page.

#### E2: No sitemap.xml or malformed sitemap

**Frequency:** Common. About 6 in 10 projects.

**What it looks like:** The app has no `sitemap.xml`, or the sitemap exists but lists only the root URL, or it returns a 404. Google Search Console shows "Couldn't fetch" errors.

**How to verify:**
```bash
curl -s https://yourdomain.com/sitemap.xml | head -20
```

**How to fix:** Generate a static sitemap covering all public routes. For dynamic content, use a sitemap generator that runs at build time or serves dynamically. Submit to Google Search Console.

#### E3: Missing canonical URLs

**Frequency:** Moderate. About 3 in 10 projects.

**What it looks like:** Pages accessible at multiple URLs (with/without trailing slash, with/without www, with query params) all serve the same content with no `<link rel="canonical">`. Search engines treat them as duplicate content.

**How to verify:** Check page source for `<link rel="canonical" ...>`. If absent, duplicates are likely.

**How to fix:** Add a canonical tag to every page pointing to the preferred URL. Configure redirects for www/non-www and trailing slash consistency.

#### E4: Client-rendered content invisible to crawlers

**Frequency:** Common. Inherent to all SPAs without SSR.

**What it looks like:** Google's crawler (and AI crawlers like GPTBot) see an empty `<div id="root"></div>` with no meaningful content. Pages get "Crawled - currently not indexed" status in GSC.

**How to verify:** View source (not Inspect Element). If the main content is missing, crawlers see the same empty shell.

**How to fix:** Prerender critical pages, add SSR for key landing pages, or use a prerendering service. At minimum, ensure meta tags and structured data are in the static HTML.

### Code quality drift

#### Q1: Massive single-file components

**Frequency:** Very common. The most frequent code quality finding.

**What it looks like:** AI generators tend to put everything in one file. We regularly find React components over 500 lines with inline styles, business logic, API calls, and UI rendering all mixed together. One audit turned up a 1,200-line component that handled form validation, API requests, state management, and rendering.

**How to verify:**
```bash
find src/ -name "*.tsx" -exec wc -l {} + | sort -rn | head -10
```
Anything over 300 lines deserves a split.

**How to fix:** Extract hooks for logic, create smaller presentational components, move API calls to a service layer. The code works the same, but future changes become possible without breaking everything.

#### Q2: Duplicated logic across components

**Frequency:** Common. About 5 in 10 projects.

**What it looks like:** The same fetch-and-format pattern repeated in multiple components because each was generated in a separate prompt. Auth checks, date formatting, error handling duplicated three or four times.

**How to verify:**
```bash
grep -rn "supabase.from" src/components/ | wc -l
```
If the count is high relative to your number of tables, duplication is likely.

**How to fix:** Create shared hooks (`useAuth`, `useFetch`), utility functions, and a service layer. Vibecoded apps benefit from a refactoring pass after the initial generation.

#### Q3: Console.log statements left in production

**Frequency:** Common. About half of audited projects.

**What it looks like:** Debug logging scattered throughout the codebase. Some log sensitive data (user emails, API responses, tokens).

**How to verify:**
```bash
grep -rn "console.log" src/ | wc -l
```

**How to fix:** Remove debug logs or use a proper logging library with log levels. Set up a lint rule (`no-console`) to catch future additions.

### Performance anti-patterns

#### P1: Unoptimized images and missing lazy loading

**Frequency:** Very common. Present in most projects.

**What it looks like:** Full-resolution images loaded on every page, no `loading="lazy"`, no srcset for responsive sizes. Lighthouse performance score drops 15-30 points from images alone.

**How to verify:** Run Lighthouse. Check the "Properly size images" and "Defer offscreen images" audits.

**How to fix:** Compress images, use modern formats (WebP/AVIF), add `loading="lazy"` to below-fold images, implement responsive srcset.

#### P2: No code splitting

**Frequency:** Common. About 5 in 10 projects.

**What it looks like:** The entire app ships as a single JavaScript bundle. Users downloading a 2MB bundle to view a landing page. Initial load time suffers, especially on mobile.

**How to verify:** Check your build output size. In Vite:
```bash
npx vite build --report
```

**How to fix:** Use `React.lazy()` and `Suspense` for route-level code splitting. Most vibecoding tools generate this correctly if prompted, but the default output often skips it.

#### P3: Unnecessary re-renders and missing memoization

**Frequency:** Moderate. About 3 in 10 projects.

**What it looks like:** Components re-render on every parent state change because props are not memoized. Lists of 100+ items re-render entirely when a single item changes.

**How to verify:** Use React DevTools Profiler. Highlight updates and watch for components that re-render without visible reason.

**How to fix:** Use `React.memo`, `useMemo`, and `useCallback` where profiling shows unnecessary renders. Do not apply them everywhere blindly.

### Accessibility blind spots

#### A1: Missing alt text on images

**Frequency:** Very common. Present in nearly every project.

**What it looks like:** `<img>` tags with empty or missing `alt` attributes. Decorative images not marked with `alt=""` and `role="presentation"`.

**How to verify:**
```bash
grep -rn '<img' src/ | grep -v 'alt='
```
Or run axe-core in your browser dev tools.

**How to fix:** Add descriptive alt text to informational images. Use `alt=""` for decorative images.

#### A2: Poor color contrast ratios

**Frequency:** Common. About 5 in 10 projects.

**What it looks like:** Light gray text on white backgrounds, placeholder text barely visible, buttons with insufficient contrast. AI generators optimize for "clean" aesthetics that often fail WCAG AA (4.5:1 for normal text).

**How to verify:** Run axe-core or Lighthouse accessibility audit. Check contrast ratios manually with a tool like WebAIM's contrast checker.

**How to fix:** Adjust your color palette to meet WCAG AA minimums. This usually means darkening text or increasing background contrast.

#### A3: Missing keyboard navigation support

**Frequency:** Moderate. About 4 in 10 projects.

**What it looks like:** Custom dropdowns, modals, and interactive elements that only respond to mouse clicks. Tab order is broken or skips elements. No visible focus indicators.

**How to verify:** Put your mouse away. Navigate the entire app using only Tab, Enter, Escape, and arrow keys.

**How to fix:** Use semantic HTML (`<button>`, `<select>`, `<dialog>`) instead of `<div onClick>`. Add `tabIndex`, `aria-*` attributes, and visible focus styles.

## How to use this catalog

Pick the category most relevant to your launch timeline:

1. **Pre-launch (security first):** Run through S1-S4. A single missing RLS policy can expose your entire database.
2. **Post-launch (SEO):** Address E1-E4 so search engines and AI models can actually find and index your pages.
3. **Growth phase (performance + accessibility):** Tackle P1-P3 and A1-A3 as traffic increases.
4. **Ongoing (code quality):** Q1-Q3 compound over time. Address them before adding new features.

Or run a full audit at [Audit Vibe Coding](https://auditvibecoding.com) to get a scored report covering all categories with prioritized fixes.

## Contributing

Found a pattern we missed? Spotted something we got wrong? Open an issue or submit a PR. This is a living document and we update it as the Inithouse lab ships new products and runs new audits across our growing portfolio.

## Changelog

- **2026-06-05:** Initial v1 published. 16 patterns across 5 categories (Security, SEO, Code Quality, Performance, Accessibility).
