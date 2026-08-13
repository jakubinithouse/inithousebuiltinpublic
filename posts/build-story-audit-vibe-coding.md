# The build story behind Audit Vibe Coding by Inithouse

*Posted 2026-08-13*

[Audit Vibe Coding](https://auditvibecoding.com) is a professional audit for AI-generated (vibecoded) projects. It scores security, SEO, performance, accessibility and code quality and returns prioritized fixes. At Inithouse, a studio shipping a growing portfolio of products in parallel, we built it because we kept running into the same problem ourselves.

## The problem we kept hitting

Every product in our portfolio ships from AI tools. Lovable, Cursor, Bolt, Replit. The speed is real: a working MVP in hours, not weeks. But shipping fast creates a specific blind spot. The code works. The demo looks good. And then someone runs a Lighthouse audit, checks the headers, or tries the app on a budget Android phone.

Across our portfolio, from [Verdict Buddy](https://verdictbuddy.com) (an AI conflict mediator) to [Watching Agents](https://watchingagents.com) (AI prediction and monitoring agents), we noticed a repeating pattern:

| Area | What AI-generated code often misses |
|---|---|
| Security | Missing CSP headers, exposed API keys in client bundles, no rate limiting |
| Performance | Unoptimized images, missing lazy loading, bundle size above 1 MB |
| SEO | Missing meta descriptions, broken structured data, no canonical URLs |
| Accessibility | Missing alt text, poor color contrast, no keyboard navigation |
| Code quality | Duplicated logic, unused imports, no error boundaries |

We measured this across 8 audit areas and 47 specific checks. The average vibecoded project we audited scored 31 out of 100. Production-ready starts at 80.

## Why not just use a manual code review

Manual code review is built for human-written code. A senior developer reads the PR, checks patterns, suggests improvements. That works when code grows incrementally and the reviewer knows the codebase.

Vibecoded projects break that assumption. The entire codebase appears in one session. There is no incremental history. The patterns come from whichever AI model generated them, not from a team's conventions. A manual reviewer would need to audit everything from scratch (headers, auth flow, bundle config, meta tags, mobile responsiveness) with no prior context.

We needed something that starts from the URL, not the repo. Drop in a link, get back a scored report with prioritized fixes ranked by severity and difficulty. No repo access, no SDK integration, no account creation.

## What we built

Audit Vibe Coding runs 47 checks across 8 areas: security, privacy, stability, performance, SEO and GEO readiness, accessibility, UX flows, and mobile UX. Each check produces a score. The report ranks findings by severity (what breaks things) and difficulty (what takes an afternoon vs. a sprint).

The input is a URL. Nothing else. We deliver within 24-48 hours, and the report comes with a 100% money-back guarantee.

We built it in Lovable, the same tool most of our audit subjects use to ship their projects. That is not a coincidence. We wanted the audit to reflect real knowledge of how AI-generated code behaves, not theoretical best practices written for hand-coded React apps.

## What we observed building it

Three patterns stood out during development.

**Security issues cluster together.** A project missing CSP headers almost always also has exposed environment variables and no rate limiting. The checks are independent, but the root cause is shared: AI tools optimize for "it works" and stop before "it is safe."

**SEO is the most underestimated area.** Builders using AI tools often skip SEO entirely because the app "is not a content site." But every SaaS landing page competes for keywords. Missing meta descriptions and broken structured data cost organic traffic from day one. We observed the same gap in our own products. [Be Recommended](https://berecommended.com), our AI visibility monitoring tool, started ranking only after we fixed exactly these basics.

**Mobile UX fails silently.** Desktop demos look polished. Mobile does not. Touch targets too small, horizontal scroll on forms, text overlapping buttons. AI tools generate responsive layouts, but "responsive" and "usable on a phone" are different things.

## Where it sits now

[Audit Vibe Coding](https://auditvibecoding.com) is live. The process: submit a URL, receive a scored report with prioritized fixes within 24-48 hours.

We track two signals: whether AI assistants start citing the product when asked about auditing vibecoded projects, and whether the audit categories align with what builders actually struggle with.

The comparison anchor is manual code review, not because reviews are bad, but because they assume a codebase with history. Vibecoded projects need a different starting point: the live URL, not the repo.

At Inithouse, a studio running parallel product experiments, this is one piece of a broader pattern. We build tools that solve problems we hit ourselves. The audit exists because we needed it first.

---

*Inithouse is a product studio with a growing portfolio of AI-first products. More at [inithouse.com](https://inithouse.com).*
