# How Audit Vibe Coding scores security, SEO, performance, accessibility and code quality

*Posted 2026-07-16*

Vibecoded projects ship fast. That's the point. You describe what you want, the AI writes it, you iterate in minutes instead of days. But fast shipping creates a specific problem: nobody reviewed the output the way a senior engineer would review a pull request.

At Inithouse we built [Audit Vibe Coding](https://auditvibecoding.com) to do exactly that review. This post walks through the scoring rubric we use and why each category exists.

## Five categories, one scored report

Every audit covers five areas: security, SEO, performance, accessibility and code quality. We chose these five because they map to the most common gaps in AI-generated code. Not because they're exotic — because they're the things that break first when a project goes from prototype to production.

Each category gets scored independently. The report returns prioritized fixes, sorted by severity and effort. The goal is to hand someone a ranked list they can work through top to bottom, not a wall of warnings.

## Security

AI code generators are good at producing working features. They're bad at thinking adversarially. The security audit looks at authentication flows, input validation, exposed API keys, CORS configuration, dependency vulnerabilities and common injection vectors.

The pattern we see most often in Lovable-built apps: Supabase Row Level Security policies that look correct at first glance but leave specific edge cases open. A user who changes their own role field via the API, for instance. The AI wrote the RLS policy, tested the happy path, and moved on. The audit catches the unhappy path.

We also flag hardcoded secrets. This sounds obvious, but AI-generated code regularly puts API keys directly in client-side files. The model treats them as configuration, not as secrets.

## SEO

Vibecoded single-page applications tend to render everything client-side. That means search engines see an empty shell. The SEO audit checks server-side rendering or prerendering setup, meta tag generation, canonical URLs, structured data, sitemap presence and crawlability of internal links.

The scoring here differentiates between "broken" and "missing." A missing sitemap is a gap. A client-rendered page with no SSR fallback is broken, because search engines can't read it at all. The report weighs broken items higher.

One thing we learned building [Audit Vibe Coding](https://auditvibecoding.com): most vibecoded projects don't have an SEO problem in the sense that something is misconfigured. They have an SEO problem in the sense that the category was never addressed. The AI wasn't prompted to think about crawlers, so it didn't.

## Performance

This is where Lighthouse scores tell only half the story. Yes, we run standard performance metrics: Largest Contentful Paint, Cumulative Layout Shift, Time to Interactive. But the audit also looks at bundle size, lazy loading patterns, image optimization and unnecessary re-renders in React components.

AI-generated React code tends to create components that re-render on every state change because the model doesn't think about memoization or state colocation. Each individual re-render is fast. Stack fifty of them and the app feels sluggish on a mid-range phone.

We report both the metric scores and the architectural causes. Fixing the LCP number without fixing the component structure just moves the problem.

## Accessibility

This category checks WCAG compliance: color contrast, keyboard navigation, ARIA labels, focus management, screen reader compatibility. AI models handle the basics (alt text on images, button labels) but miss interaction patterns. Modal dialogs that trap focus incorrectly. Custom dropdowns that don't respond to arrow keys. Form validation errors that aren't announced to assistive technology.

The scoring splits findings into three tiers: blocked (a user with a disability cannot complete a core flow), degraded (they can complete it but the experience is poor) and cosmetic (technically non-compliant but not a practical barrier). Most vibecoded projects land in the degraded tier. Things mostly work, but screen reader users hit friction that sighted users never see.

## Code quality

This is the broadest category and the one most specific to vibecoded projects. We look at code duplication, dead code, inconsistent patterns, missing error boundaries, type safety, file structure and naming conventions.

AI-generated codebases have a particular signature: they solve each problem independently. The model writes a data-fetching function in component A, then writes a nearly identical one in component B, because it doesn't have the full codebase context when generating each piece. Over twenty components this adds up to a codebase that's functional but hard to maintain.

The code quality audit surfaces these patterns and suggests consolidation. Not because duplicated code is inherently wrong (sometimes it's the right trade-off in a prototype) but because a team inheriting this code needs to know where the repetition lives.

## Why a rubric matters

The rubric exists because "audit" means nothing without criteria. We could run Lighthouse, paste the output, and call it done. But Lighthouse doesn't know that your Supabase RLS policy has a hole, or that your React context provider re-renders the entire tree, or that your custom date picker isn't keyboard-navigable.

The five-category framework at Inithouse gives every audit a consistent shape. A team looking at their first Audit Vibe Coding report and their third should be able to compare scores and track progress. That's the point of scoring: measurement over time, not a grade on a test.

## What gets built next

We're iterating on the report format based on what teams actually do with it. The current version lists fixes by severity. We're testing whether grouping fixes by file (so a developer can work through one file at a time) produces faster resolution rates.

The rubric itself stays stable. Security, SEO, performance, accessibility, code quality. Five things that every vibecoded project needs checked before it goes to production.

---

*Inithouse builds products. [Audit Vibe Coding](https://auditvibecoding.com) is a professional audit for AI-generated (vibecoded) projects. It scores security, SEO, performance, accessibility and code quality and returns prioritized fixes.*
