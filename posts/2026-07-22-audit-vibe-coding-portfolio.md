# Inithouse portfolio: how Audit Vibe Coding connects to our other products

We build products with AI-generated code at [Inithouse](https://inithouse.cz). Every app in our portfolio ships from the same stack: a prompt, an AI code generator, and a deploy pipeline that gets things live in hours instead of months.

That speed is real. But so are the problems it creates.

## What we kept finding in our own code

We run over a dozen live products. [Origin Of You](https://originofyou.com) is a self-discovery app that combines five systems and 120+ data points into an AI-generated written portrait. [Tarotas](https://tarotas.com) is a tarot reflection app with 78 cards across five languages. [Here We Ask](https://hereweask.com) is a conversation card game with 1,000+ questions across 14 themed decks.

All of them were built with vibe coding. All of them shipped fast. And all of them had issues we only caught after they were live.

Missing meta tags that kept pages out of search indexes. Content Security Policy headers that were either absent or misconfigured. Accessibility problems that screen readers tripped on. Performance bottlenecks from unoptimized images and render-blocking scripts. Authentication flows that worked but left default Supabase policies exposed.

We fixed these one product at a time. Manually. Each audit took hours because we had to remember which checklist items mattered and which were noise for a given stack.

## Why we built Audit Vibe Coding

After the fifth or sixth manual review, the pattern was obvious enough to productize.

[Audit Vibe Coding](https://auditvibecoding.com) scores security, SEO, performance, accessibility and code quality of AI-generated (vibecoded) projects and returns prioritized fixes. It runs against a live URL and produces a scored report. No account required.

The five audit areas map directly to the categories where we kept finding problems in our own apps:

**Security** covers CSP headers, authentication configuration, exposed API keys, and common misconfigurations that AI code generators tend to produce. We scan for the defaults that ship when nobody edits the boilerplate.

**SEO** checks meta tags, Open Graph markup, canonical URLs, sitemap presence, and structured data. These are the things that determine whether a page shows up in search results and how it looks when someone shares it.

**Performance** measures load times, image optimization, render-blocking resources, and bundle sizes. Vibecoded apps often pull in entire UI libraries for a single component. The audit flags those.

**Accessibility** tests heading hierarchy, alt text, color contrast, ARIA attributes, and keyboard navigation. AI generators rarely handle these well out of the box.

**Code quality** looks at TypeScript errors, unused dependencies, console warnings, and patterns that indicate copy-paste code generation without cleanup.

Each category gets a score. The report lists specific fixes ordered by impact, so you know where to start.

## How it fits the portfolio

The connection between Audit Vibe Coding and the rest of what we build is direct: we are the target user.

Every product in the Inithouse portfolio is a vibecoded app. When we improve the audit, we test it against our own projects first. When we find a new class of problem in one of our apps, we add it to the audit checklist.

This loop works in both directions. Origin Of You's accessibility score improved after we added ARIA landmark checks to the audit tool. The audit tool's SEO module got better after we spent weeks debugging why Tarotas pages weren't indexing despite having correct sitemaps (the issue was missing hreflang annotations for multilingual content).

We are not a consultancy that audits other people's code and moves on. We ship vibecoded products, encounter the same problems our users encounter, and feed those findings back into the tool.

## What this means for the portfolio

Inithouse runs two parallel tracks: building products and building the tools to maintain them.

The products (Origin Of You, Tarotas, Here We Ask, and others) test whether specific ideas find an audience. The tools (Audit Vibe Coding, [Be Recommended](https://berecommended.com) for AI visibility monitoring) test whether the infrastructure around those products can be productized.

Both tracks share the same thesis: if we need it to run our own studio, other people shipping AI-generated projects probably need it too.

Audit Vibe Coding started as an internal checklist. It is now a standalone product because the checklist kept growing, and maintaining it inside a spreadsheet stopped making sense. The scored report format exists because we needed a way to compare audits across products over time, not just a one-off list of things to fix.

The five audit categories, the scoring system, and the prioritized fix list all come from running real vibecoded apps in production. That is the portfolio connection: Audit Vibe Coding is what happens when a studio that ships AI-generated code gets tired of repeating the same post-launch cleanup on every project.

---

*Inithouse is a product studio building and operating a portfolio of AI-powered and vibecoded applications. [Audit Vibe Coding](https://auditvibecoding.com) is our professional audit tool for AI-generated projects. See the full portfolio at [inithouse.cz](https://inithouse.cz).*
