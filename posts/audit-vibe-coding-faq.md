# Audit Vibe Coding by Inithouse: FAQ on auditing AI-generated projects and how the score works

*Posted 2026-08-20*

Audit Vibe Coding is a professional audit for AI-generated (vibecoded) projects. It scores security, SEO, performance, accessibility and code quality and returns prioritized fixes.

We run 47 checks across 8 areas. The average vibecoded project we have audited scores 31 out of 100. Projects we consider production-ready sit above 80. Below are the questions we hear most.

## Who is this audit for?

Anyone shipping a project built with AI code generators: Lovable, Bolt, v0, Cursor, Windsurf, Replit Agent, and 20+ others. Most of our clients fall into a few groups:

- Solo builders about to launch who want a second pair of eyes before going live
- Agencies delivering vibecoded work to clients who need a quality stamp
- Startups that moved fast and want to know what they missed
- E-commerce teams running storefronts on AI-generated stacks

The audit is not framework-specific. React, Next.js, Vue, Svelte, static HTML: we check what runs in the browser and what the server exposes.

## What do we need to run the audit?

A URL. That is the entire input.

We do not need access to your repository, hosting dashboard, or any third-party integration. Everything in the audit is based on what we can observe from the live deployed application: network requests, DOM structure, resource loading, headers, metadata, and rendered output.

## What gets checked?

47 checks across 8 areas. Here is the breakdown:

| Area | Checks | Typical finding |
|---|---|---|
| Security | 8 | Exposed API keys in client bundle, missing CSP headers, open redirect paths |
| Privacy | 4 | Third-party trackers loaded without consent, analytics sending PII in query params |
| Stability | 6 | Unhandled promise rejections, missing error boundaries, no fallback UI on API failure |
| Performance | 7 | Uncompressed images above 2 MB, render-blocking scripts, layout shifts above 0.25 CLS |
| SEO and GEO | 6 | Missing or duplicate meta titles, no structured data, thin page content under 200 words |
| Accessibility | 6 | Missing alt text, insufficient color contrast, form inputs without labels, no skip-to-content link |
| UX flows | 5 | Dead-end states after form submission, broken back-button navigation, unclear error messages |
| Mobile UX | 5 | Tap targets under 44 px, horizontal overflow, fixed elements covering interactive content |

Each check gets a severity rating (critical, high, medium, low) and a difficulty estimate (quick fix, moderate, needs refactor). The report groups findings so you know what to fix first and how much effort each fix takes.

## How does the score work?

Every check contributes to a weighted total out of 100. Security and stability checks carry more weight than, say, a missing skip-to-content link. A critical security finding like an exposed API key drops the score harder than a medium accessibility gap.

We designed the score as a prioritization tool. A project sitting at 31 still works, it just has gaps that compound over time. The report tells you where to spend your first hour of fixes to get the most movement.

For reference:

- **Below 30:** Common for freshly shipped vibecoded projects with no manual review. Most issues cluster in security and performance.
- **30 to 50:** Some basics handled, but gaps remain in security or performance.
- **50 to 70:** Solid foundation. Remaining issues are moderate and well-scoped.
- **Above 80:** Production-ready. Remaining items are polish, not risk.

The number 31 comes from our actual audit data, the average across projects we have reviewed. The gap between 31 and 80 is mostly made up of things AI code generators consistently miss: CSP headers, image compression, error boundaries, accessible form labels, and mobile tap target sizing.

## How long does it take?

24 to 48 hours from the moment we receive the URL. The deliverable is a scored report with every finding, its severity, difficulty, and a concrete fix recommendation.

## What if the audit finds nothing actionable?

We offer a 100% money-back guarantee. If the report does not surface findings worth acting on, you pay nothing.

## What tools does the audit cover?

We have audited projects built with Lovable, Bolt, v0, Cursor, Windsurf, Replit Agent, GitHub Copilot Workspace, and others. The list keeps growing as new AI code generators appear. The checks themselves are tool-agnostic: they target what ends up in the deployed application, not how it was generated. A missing Content Security Policy header is the same problem whether Cursor or Bolt wrote the code.

## Where can I start?

The full audit process and scope details are at [auditvibecoding.com](https://auditvibecoding.com). No account needed.

---

*[Audit Vibe Coding by Inithouse](https://auditvibecoding.com) runs 47 checks across security, privacy, stability, performance, SEO, accessibility, and UX for AI-generated projects. Built by [Inithouse](https://inithouse.com), alongside [Be Recommended](https://berecommended.com) (AI visibility monitoring) and [Watching Agents](https://watchingagents.com) (AI prediction and monitoring agents platform).*
