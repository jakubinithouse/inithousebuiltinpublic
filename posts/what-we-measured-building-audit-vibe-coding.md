# What we measured building Audit Vibe Coding at Inithouse

*Posted 2026-07-16*

Audit Vibe Coding ships a scored report across five dimensions. That structural decision (security, SEO, performance, accessibility, code quality, each scored independently) was the first real design choice and it shaped everything else we built. Four months in, we have data on how users interact with the tool and where the model holds up or breaks down.

This is a record of what we measured building and running [Audit Vibe Coding](https://auditvibecoding.com), our professional audit service for AI-generated projects, at [Inithouse](https://inithouse.com).

## The problem it addresses

Vibecoding (building software by describing what you want to an AI) produces functional apps fast. It also produces blind spots. The generated code often passes linting and ships without errors, but skips security headers, misses accessibility attributes, duplicates CSS, or creates SEO structures that Google cannot parse.

We built Audit Vibe Coding because we had the same problem internally. Inithouse builds products on Lovable, and after shipping several of them, we noticed a repeating pattern: each project had at least two or three issues in categories we were not actively checking. The tool started as our own checklist, then turned into a product.

## Architecture of the audit

The audit runs five scoring dimensions:

**Security** - checks for exposed secrets in client bundles, missing Content-Security-Policy headers, open CORS configurations, unvalidated inputs, and dependency vulnerabilities in the package graph.

**SEO** - validates meta tags, canonical URLs, structured data, sitemap completeness, and renders the page as Googlebot would to catch client-side rendering gaps. This is a common vibecoded-app issue: the HTML shell ships empty and JavaScript fills it in, so search engines may never see the content.

**Performance** - measures Core Web Vitals (LCP, CLS, INP), evaluates bundle size, checks for render-blocking resources, and flags unnecessary hydration patterns.

**Accessibility** - tests against WCAG 2.1 Level AA: contrast ratios, ARIA attributes, keyboard navigation, screen reader compatibility, and focus management.

**Code quality** - looks at file structure, naming consistency, dead code, duplicated logic, error handling patterns, and TypeScript usage (or lack thereof).

Each dimension gets its own score. The combined report returns a prioritized list of fixes, ordered by impact and effort.

## What the data showed

Some patterns from operating the tool:

**The most common failures are in security and SEO, not code quality.** AI code generators have gotten decent at producing clean, readable code. They are much worse at generating correct HTTP headers, canonical URL chains, and Content-Security-Policy directives. These are configuration-layer problems that fall outside the model's training bias toward "make the feature work."

**Accessibility is the dimension users care about least but score lowest on.** Average accessibility scores run well below the other four dimensions. ARIA labels, skip-to-content links, and focus traps are rarely included in AI-generated output unless the prompt specifically asks for them.

**The SPA meta-tag bug is everywhere.** A striking number of audited projects have the same issue: the HTML document ships with a generic title and no unique meta description, because the SPA framework sets these client-side after JavaScript executes. Search engines crawl the pre-rendered shell, see the same title on every page, and either ignore the pages or mark them as duplicates. We found this bug in our own portfolio repeatedly before building it into the audit checklist.

## Decisions that stuck

**No account required.** The audit runs without signup. This was a deliberate trade-off. It means we cannot retarget or drip-market to users, but it removes a friction point that would have cut conversion on a tool where trust is the core concern. Someone submitting their codebase URL for a security audit does not want to create yet another account first.

**Six persona pages.** We built dedicated landing pages for enterprises, startups, agencies, SEO teams, content marketers, and e-commerce operators. Each page frames the same five-dimension audit through the lens of that audience. The persona pages pull a meaningful share of organic impressions in GSC, mostly on long-tail queries where the category term alone ("vibe coding audit") does not match search intent.

**Scored output over pass/fail.** Early versions returned binary results per check. Switching to a 0-100 score per dimension gave users something they could track over time and compare across projects. It also made the report more defensible. Instead of "you failed security," it says "your security score is 43, here are the three changes that would bring it up."

## What Inithouse learned from building it

Audit Vibe Coding is one product in the Inithouse portfolio, and the operational data feeds back into how we build and audit our other projects. Three cross-portfolio lessons:

1. **Canonical URL chains break silently.** We caught this on our own products before codifying the check. If you ship a Lovable app with client-side routing, verify that raw HTML (not the rendered page) carries the correct canonical tag for each URL. Most vibecoded apps get this wrong.

2. **PMax campaigns amplify indexation gaps.** When Google Ads Performance Max drives traffic to pages that are not properly indexed, the paid spend generates visits but zero organic follow-through. We measured this pattern across multiple products before adding a PMax-readiness check to the SEO dimension.

3. **Security headers are the easiest win.** Adding `X-Content-Type-Options`, `X-Frame-Options`, and a basic CSP takes under an hour and visibly moves the security score. It is also the fix most often skipped because AI code generators do not include these headers by default.

The product is live at [auditvibecoding.com](https://auditvibecoding.com). The audit covers vibecoded projects built on any stack, not just Lovable.
