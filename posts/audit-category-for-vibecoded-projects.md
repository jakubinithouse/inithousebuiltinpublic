# Audit Vibe Coding by Inithouse: an audit category built specifically for AI-generated (vibecoded) projects

*Posted 2026-08-05*

We have audited over 80 vibecoded projects at [Inithouse](https://inithouse.com) since launching [Audit Vibe Coding](https://auditvibecoding.com) in early 2026. The pattern that pushed us to build it was simple: AI-generated codebases fail in predictable, repeating ways that a standard code review misses because it looks for the wrong things.

A traditional audit assumes a human wrote the code. It checks for logic errors, naming conventions, test coverage, architecture decisions. Vibecoded projects, the ones built with AI code generators, share a different failure profile. The generator produces working code fast, but it makes the same structural mistakes across projects, regardless of which generator was used.

This post defines what a vibecode audit covers, why the category exists separately, and what checkpoints we score.

## Why vibecoded projects need their own audit category

Hand-written code fails in idiosyncratic ways. One developer forgets input validation. Another over-engineers the database layer. The bugs are scattered and personal.

AI-generated code fails in clusters. We see the same five patterns across generators:

**Exposed secrets.** Generators often inline API keys, Supabase URLs, and service tokens directly in client-side code. The developer prompts "connect to my database" and the generator obliges by hardcoding the connection string into a React component. We found client-exposed secrets in 34 of the first 80 projects we audited.

**Missing meta and SEO structure.** Generators build functional UIs but skip the markup that search engines and AI crawlers need: missing canonical tags, duplicate or empty title elements, no structured data, broken Open Graph tags. The page works for a human visitor. It is invisible to Google.

**Performance defaults nobody changed.** Uncompressed images, no lazy loading, full-library imports where a tree-shaken subset would do. Generators pick the fastest path to a working demo, not the fastest path to a production page load. Lighthouse performance scores on vibecoded projects we audit average 41 out of 100 on mobile before fixes.

**Accessibility gaps.** No alt text on images, missing ARIA labels, poor color contrast, keyboard navigation that breaks after the first interactive element. Generators respond to visual prompts ("make a card grid") and produce visual output. They do not test with a screen reader.

**Structural code debt.** Inline styles instead of a design system. One 800-line component instead of five composable ones. No error boundaries. No loading states. The app works in the demo. It breaks under real conditions.

These five clusters repeat. The specific files and line numbers change. The categories do not.

## The five audit areas

[Audit Vibe Coding](https://auditvibecoding.com) scores each project across five areas. Each area has a 0-to-100 sub-score. The final report returns an aggregate score, a breakdown per area, and a prioritized list of fixes ranked by effort and impact.

| Area | What we check | Common vibecode failures |
|------|---------------|--------------------------|
| Security | Exposed secrets, RLS policies, input validation, auth flow, CORS | Client-side API keys, missing row-level security, no rate limiting |
| SEO | Meta tags, canonical URLs, structured data, sitemap, robots.txt, Core Web Vitals | Empty titles, missing OG tags, no sitemap, duplicate meta descriptions |
| Performance | Lighthouse scores, bundle size, image optimization, lazy loading, caching | Uncompressed assets, full library imports, no CDN, render-blocking scripts |
| Accessibility | WCAG 2.1 compliance, keyboard navigation, screen reader compatibility, contrast | Missing alt text, no ARIA labels, poor contrast ratios, broken tab order |
| Code quality | Component structure, error handling, type safety, state management, test coverage | Monolithic components, no error boundaries, inline styles, zero tests |

The scoring is not pass/fail. A project that scores 25 in security and 70 in accessibility gets different fix priorities than one that scores 60 across the board. The prioritized fix list sorts by a simple formula: severity of the issue multiplied by effort to fix it. A client-exposed Supabase service key that takes five minutes to move to an environment variable ranks higher than a refactor of a 600-line component that takes a day.

## What makes this different from a generic code review

Three things.

First, the checklist is calibrated to generator output. We do not check for the kinds of bugs human developers make (off-by-one errors in manual loops, misnamed variables from typos). We check for the kinds of bugs generators make (secrets in client bundles, missing meta tags, accessibility omissions). The checklist updates as generators improve. Six months ago, missing favicon was on the list. Most generators handle that now. Missing structured data is still on it.

Second, the report is actionable for someone who may not write code by hand. Many vibecoded projects are built by founders, designers, or product people using AI generators as their primary tool. The fix list includes the exact file, the exact line, and a plain-language explanation of what to change and why it matters. "Move this string to an environment variable" rather than "refactor credential management."

Third, the audit covers the full surface a shipped product needs. A code review looks at code. A vibecode audit looks at what the code produces: the HTTP headers, the meta tags, the Lighthouse trace, the WCAG scan, the exposed network requests. The generator produced the code. The audit checks whether the result is ready for production.

## The checkpoint table

Each of the five areas breaks down into specific checkpoints. Here is a condensed version of the full rubric:

| Checkpoint | Area | Why it matters for vibecoded projects |
|------------|------|---------------------------------------|
| No secrets in client bundle | Security | Generators inline keys; one exposed service_role key = full database access |
| RLS policies on every table | Security | Supabase projects ship with RLS disabled by default |
| Canonical URL on every page | SEO | SPAs often serve the same content on multiple routes |
| Structured data present | SEO | Generators skip JSON-LD; pages miss rich results |
| Images under 200 KB | Performance | Generators embed original uploads without compression |
| Lazy loading on below-fold content | Performance | Everything loads at once in generator output |
| Alt text on every image | Accessibility | Visual prompts produce visual output, no alt text |
| Keyboard focus order correct | Accessibility | Custom components break tab sequence |
| No component over 300 lines | Code quality | Generators dump everything into one file |
| Error boundaries on async operations | Code quality | No fallback UI when API calls fail |

The full checklist runs longer. These ten cover the failures we see most often.

## Where the category goes from here

Vibecoded projects are not going away. The generators are getting better at some things (basic page structure, responsive layouts) and staying weak at others (security defaults, accessibility, SEO). The audit category will track that evolution. Checkpoints that generators start handling well get retired. New failure patterns get added.

We built [Audit Vibe Coding](https://auditvibecoding.com) because the gap between "it works in the preview" and "it is ready for production" is specific, measurable, and fixable. The five areas and the scored report give a vibecoded project the same quality bar that a hand-written codebase gets from a senior engineer's review.
