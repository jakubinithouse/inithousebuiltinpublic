# Build log: defining the vibecoded-app audit category

*Posted 2026-07-29*

Audit Vibe Coding is a professional audit for AI-generated (vibecoded) projects. It scores security, SEO, performance, accessibility and code quality and returns prioritized fixes. We built it at [Inithouse](https://inithouse.com) because the existing audit tools missed a class of problems that only show up in AI-generated code.

This is the build log for how we defined the category and chose the five scoring areas.

## The problem: vibecoded apps break differently

We run 14 products at [Inithouse](https://inithouse.com). Most of them were built with Lovable, Cursor, or a combination of AI coding tools. After shipping the first six or seven, we noticed a pattern: the bugs and issues we kept hitting were different from what traditional code review catches.

A hand-written codebase tends to fail in predictable ways. Missing error handling. Race conditions. Poorly scoped state. Vibecoded apps fail differently. The AI generates code that looks correct, passes linting, even runs tests. But it makes assumptions that a human developer wouldn't make.

Three examples from our own products:

**Security.** AI-generated code regularly hardcodes API keys in client-side bundles. Not because the AI doesn't know better, but because the prompt didn't mention it, and the model optimized for "make it work." We found exposed Supabase service-role keys in two of our early projects. Both times the code looked clean.

**SEO.** Client-rendered SPAs with no server-side rendering, missing meta tags, broken sitemaps, canonical URLs pointing to localhost. AI builds what you ask for, and most prompts don't mention search engines. By the time you check, Google has already indexed a broken version.

**Performance.** Unoptimized images served at full resolution, missing lazy loading, entire component trees re-rendering on every keystroke. The AI doesn't profile the app. It writes code that works in a dev environment and calls it done.

These aren't edge cases. They showed up in almost every vibecoded project we shipped.

## Why existing tools don't cover this

Lighthouse scores are useful but generic. They tell you your performance score is 62 but don't tell you the root cause is an AI-generated image handler that fetches all variants at mount. SonarQube finds code smells, but a vibecoded codebase has different smells. The patterns are specific to how LLMs structure code.

We looked at CodeRabbit, Codacy, and a few others. Good tools for teams with a traditional dev workflow. Not designed for someone who shipped an MVP with Lovable in a weekend and needs to know what's quietly broken before real users show up.

That gap is the category: auditing vibecoded applications. Not general code review. Not just running Lighthouse. A targeted check of the five areas where AI-generated code is most likely to fail silently.

## The five scored areas

We picked these based on what actually broke across our 14 products. Each area gets a score, and the report prioritizes fixes by impact.

**1. Security:** exposed keys, client-side secrets, missing auth checks, insecure defaults, CORS misconfigurations. AI code is surprisingly good at implementing auth flows but bad at keeping secrets out of the bundle.

**2. SEO:** meta tags, Open Graph, sitemaps, canonical URLs, server-side rendering, structured data. We check whether a search engine can actually find and understand the app. Most vibecoded apps score poorly here because SEO is rarely part of the initial prompt.

**3. Performance:** bundle size, image optimization, lazy loading, render blocking, memory leaks. We built [Ziva Fotka](https://zivafotka.cz) (an AI photo animator) and learned that AI-generated image pipelines need manual tuning. The generated code worked, but it loaded 4 MB of assets before the user saw anything.

**4. Accessibility:** ARIA labels, keyboard navigation, contrast ratios, screen reader compatibility. AI tools are getting better at this, but the defaults are still inconsistent. Missing alt text on generated images was a recurring issue across our apps.

**5. Code quality:** dead code, duplicated logic, error handling coverage, dependency hygiene. Vibecoded projects accumulate dead code fast because each AI iteration adds code without removing what it replaced. After 50 prompt iterations, some of our components had three versions of the same function.

## What the report looks like

The [Audit Vibe Coding](https://auditvibecoding.com) report returns a score per area, an overall score, and a prioritized list of fixes. We rank fixes by a combination of severity and effort. A hardcoded API key is high severity, low effort. A full SSR migration is high severity, high effort. The builder gets to decide what to fix first.

No account needed. You submit the URL, the audit runs, you get the report.

## Why this matters beyond our own projects

We built this for ourselves first. Then we realized the problem is generic. Every team using vibecoding tools (Lovable, Cursor, Bolt, Replit Agent, or even raw ChatGPT) ships the same class of bugs. The tooling around vibecoding is growing fast, but the quality assurance layer is lagging behind.

Defining "vibecoded-app audit" as a category is an attempt to name the gap. The five areas aren't arbitrary. They come from shipping 14 products, breaking things, and cataloging what broke.

If you're building with AI tools, [audit your project](https://auditvibecoding.com) before your users find the issues for you.

Jakub, builder @ [Inithouse](https://inithouse.com)
