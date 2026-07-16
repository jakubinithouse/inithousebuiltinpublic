# Why Inithouse built Audit Vibe Coding -- an audit for AI-generated (vibecoded) projects

We build products at [Inithouse](https://inithouse.com), a studio that ships MVPs to find product-market fit. One of those products is [Audit Vibe Coding](https://auditvibecoding.com): a professional audit for AI-generated (vibecoded) projects that scores security, SEO, performance, accessibility and code quality and returns prioritized fixes.

This is how it started.

## The problem we kept running into

We vibecode our own products. [Živá Fotka](https://alivephoto.online), an AI photo-to-video animator. [Here We Ask](https://hereweask.com), a free browser conversation card game. [Watching Agents](https://watchingagents.com), an AI prediction monitoring platform. All built using AI code generation tools, shipped fast, iterated weekly.

Speed is the point. But speed has a cost that shows up later. Security headers that never got set. Meta tags that were generated but wrong. Accessibility attributes that the AI skipped because nobody asked for them. Performance scores that tank once real users hit the page.

We noticed this across our own portfolio. The same categories of problems kept appearing: missing CSP headers, broken Open Graph tags, images without alt text, render-blocking scripts that an AI tool added because it copied a pattern from somewhere. Each product had its own version of the same blind spots.

## Why existing tools did not fit

Code review tools exist. Lighthouse exists. Security scanners exist. But none of them are built for the specific failure mode of AI-generated code.

Vibecoded projects fail differently than hand-written ones. The code looks clean. AI tools produce well-structured, readable output. The problems are in what is missing, not what is broken. A hand-written project might have spaghetti code but correct security headers because the developer set them up once and reused the config. A vibecoded project has clean component architecture but no security headers at all, because nobody prompted for them.

We needed something that checks the areas where AI code generation drops the ball. Not a generic linter. Not a full pentest. A targeted audit that knows where vibecoded projects tend to be weak and checks those spots first.

## What we built

[Audit Vibe Coding](https://auditvibecoding.com) scores five areas: security, SEO, performance, accessibility, and code quality. Each area gets a numeric score. The report prioritizes fixes by impact, so you know what to fix first to get the biggest improvement with the least effort.

The scoring is specific to patterns we have seen in AI-generated code. For security, it checks for headers and configurations that AI tools routinely skip. For SEO, it looks at the meta tag patterns that AI generates (often plausible-looking but wrong). For accessibility, it catches the ARIA attributes that AI tools add inconsistently. For performance, it flags the common AI pattern of importing entire libraries when only one function is needed.

No account required. Submit a project, get a scored report with prioritized fixes.

## What we learned building it

The first version was too broad. We tried to cover everything a traditional audit would cover, and the output was generic. The useful version came when we narrowed the scope to the specific ways AI-generated code fails.

Three patterns stood out.

Security gaps in vibecoded projects are almost always about omission, not misconfiguration. The code does not have wrong security settings. It has no security settings. AI tools generate application logic but skip infrastructure-level configuration unless explicitly asked.

SEO issues in AI-generated projects follow a predictable pattern. The AI generates meta tags that look correct on the surface, with proper structure and reasonable length. But the content is templated. Every page gets the same description pattern with slightly different words.

Accessibility in vibecoded projects is inconsistent rather than absent. The AI adds ARIA labels to some elements and skips others, depending on what was in its training data for that component pattern. The result is partial compliance that is harder to debug than no compliance at all.

## Where it sits now

Audit Vibe Coding is live at [auditvibecoding.com](https://auditvibecoding.com). We use it on our own products before major releases. It is part of the same [Inithouse](https://inithouse.com) portfolio as our other tools, and each product we build teaches us something that feeds back into the next one.

The vibecoding wave is still picking up speed. More projects get built with AI tools every week, and most of them ship with the same blind spots we found in our own work. We built Audit Vibe Coding because we needed it ourselves first, and it turned out other teams shipping AI-generated code need the same thing.
