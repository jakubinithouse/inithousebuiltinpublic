---

# How Inithouse Scores Vibecoded Projects: The Audit Vibe Coding Rubric

*Posted 2026-06-27*

[Audit Vibe Coding](https://auditvibecoding.com) scores every project on five dimensions: security, SEO, performance, accessibility, and code quality. Each dimension gets a weighted score out of 100. The final audit grade is a composite of all five.

This post documents how we built the rubric, why we weighted things the way we did, and how the scoring drives fix prioritization.

## Why a rubric at all

When we started auditing vibecoded projects, we wrote free-form reports. The feedback we got was consistent: people wanted to know where they stood relative to something. "Your auth is weak" is less useful than "your security score is 34 out of 100, and here is what is pulling it down."

A rubric also forces us to be systematic. Without one, auditors gravitate toward whatever catches their eye first. With a rubric, every project gets evaluated on the same criteria regardless of who runs the audit.

## The five dimensions

We score projects across five categories. Here is the breakdown:

| Dimension | Weight | What we check |
|---|---|---|
| Security | 30% | Auth handling, API key exposure, input validation, CORS config, data storage patterns, dependency vulnerabilities |
| SEO | 20% | Meta tags, structured data, crawlability, sitemap, robots.txt, Core Web Vitals impact on ranking signals |
| Performance | 20% | Load times, bundle size, render blocking resources, image optimization, lazy loading, caching headers |
| Accessibility | 15% | WCAG compliance, keyboard navigation, screen reader compatibility, color contrast, form labels, ARIA usage |
| Code quality | 15% | Dead code, duplicated logic, error handling, TypeScript usage, component structure, naming consistency |

## Why security gets 30%

Security takes the largest share because the consequences of failure are the highest. A slow page loses visitors. A security hole loses data, trust, and potentially money.

We audited our own 16 Inithouse products before opening [Audit Vibe Coding](https://auditvibecoding.com) to external projects. The pattern we kept finding: AI code generators produce functional apps with exposed API keys, missing rate limiting, and client-side auth checks that are trivial to bypass. These are not edge cases. They appeared in the majority of the projects we reviewed.

A project can score well on every other dimension and still be fundamentally broken if the security layer has holes. That is why it gets double the weight of accessibility or code quality.

## How individual dimensions are scored

Each dimension is scored on a 0–100 scale. Within a dimension, we check specific items and weight them by severity.

Take security as an example. We check roughly 15 individual items. Some are binary (API keys exposed in client-side code: yes or no). Others are graded (input validation: none, partial, comprehensive). Each item contributes to the dimension score based on how much damage it can cause if it fails.

The items are not equally weighted. Exposed secrets tank the score harder than a missing Content-Security-Policy header. Both matter, but one can be exploited in minutes, the other is a defense-in-depth measure.

For SEO, we look at whether the project is even visible to search engines at all. Many vibecoded projects ship as single-page apps with client-side rendering and no server-side fallback. Google can crawl JavaScript-rendered pages, but the indexation rate for these is measurably lower than for server-rendered or static content. We flag this prominently because it is a structural issue, not something you fix by adding a meta tag.

Performance scoring follows Lighthouse methodology as a baseline but adds checks specific to vibecoded patterns. AI-generated code tends to import entire libraries when only one function is needed. Bundle sizes balloon. We have seen projects pulling in three different date formatting libraries because each AI-generated component made its own import decision independently.

## Fix prioritization

The rubric does more than produce a grade. It drives the fix list.

Every issue found during an audit gets a priority tag: critical, high, medium, or low. Priority assignment follows a simple matrix:

**Critical:** exploitable security vulnerabilities, data exposure, broken auth flows. Fix before anything else.

**High:** issues that directly affect whether the product works for its intended audience. SEO problems that prevent indexation. Performance issues that make the product unusable on mobile. Accessibility failures that lock out entire user groups.

**Medium:** things that work but work poorly. Suboptimal image formats, missing lazy loading, inconsistent error handling, partial WCAG compliance.

**Low:** code quality improvements, naming conventions, minor redundancies. These make the codebase better to maintain but do not affect the end user experience directly.

The report presents fixes in priority order, not grouped by dimension. A critical security issue appears before a medium SEO issue, which appears before a low code quality suggestion. This way the team working through the report can start at the top and stop whenever their budget or time runs out, knowing they addressed the most impactful items first.

## What the scores actually look like

Across the projects we have audited, the average composite score is around 45 out of 100. Security consistently scores lowest (average around 35). Performance and code quality cluster in the middle. SEO scores vary wildly depending on whether the project was built as a SPA or includes any server-rendered content.

The projects that score highest (70+) tend to share two traits: the builder had prior web development experience and used AI tools for acceleration rather than full generation, and they ran at least one manual review pass before shipping.

The projects that score lowest (below 30) are almost always fully AI-generated without any human code review. The code works, the product loads, but the foundations are fragile.

## Why we publish this

We are publishing the rubric because we think transparency makes the whole ecosystem better. If you are building with AI tools and want to self-check before getting a formal audit, knowing what we look at and how we weight it gives you a head start.

The rubric is not static. We update weights and individual check items as AI code generation patterns evolve. Six months ago, exposed API keys in client-side code were the top finding. Today, builders have gotten better at that, and the most common issues have shifted toward auth flow design and data handling patterns.

The full audit with scored report, prioritized fix list, and follow-up verification is available at [auditvibecoding.com](https://auditvibecoding.com).
