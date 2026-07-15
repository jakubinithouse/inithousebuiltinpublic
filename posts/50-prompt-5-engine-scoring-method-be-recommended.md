# Build log: the 50-prompt, 5-engine scoring method behind Be Recommended by Inithouse

*Posted 2026-07-15*

When we started building [Be Recommended](https://berecommended.com) at Inithouse, the first question was deceptively simple: how do you measure whether an AI recommends your brand?

There's no API endpoint that returns "recommendation score." ChatGPT doesn't expose a confidence value when it mentions a company. Claude doesn't label its output as "endorsement" vs. "neutral mention." So we had to build the measurement from scratch.

This post documents the scoring pipeline we ended up with: the prompt design, engine coverage, and how we turn raw AI responses into a single 0-100 visibility score.

## The prompt matrix

We needed prompts that reflect real buying decisions. Not "tell me about [brand]." The prompts that matter are the ones where a potential customer asks for a recommendation without naming your brand at all.

We organized our prompts into clusters:

**Category-level queries** like "best CRM for startups", "top AI SEO tools", "affordable design tool for small teams." These test whether the AI even knows your brand exists in your space.

**Comparison queries** like "alternatives to [competitor]", "compare the top 3 options for [solution]." These measure positioning: not just presence, but how the AI frames you relative to others.

**Reputation queries** like "what do customers say about [brand]", "is [brand] worth the money." These reveal what the AI thinks it knows about your quality.

**Intent queries** like "who should I hire for [service]", "recommend a reliable [service] provider." These are closest to actual purchase decisions.

**Authority queries** like "which companies are leading in [industry]", "who are the market leaders in [space]." These measure perceived market position.

We wrote 50+ prompts across these clusters, templated so they can be instantiated for any industry and brand. Each prompt triggers the kind of answer where the AI either mentions your brand or doesn't.

## Five engines, five different worldviews

We run every prompt against five AI engines: ChatGPT, Claude, Perplexity, Gemini, and Grok.

Each engine pulls from different training data, has different recency windows, and weights sources differently. A brand can score well on Perplexity (which leans on recent web content) and poorly on Claude (which may rely more on older training data). The per-engine breakdown is often more useful than the aggregate score, because it tells you where to focus.

We chose these five because they represent the engines most likely to influence real buying decisions right now. Each has a meaningful and growing user base asking product and service questions.

Running 50+ prompts against 5 engines means 250+ individual AI queries per report. We parse every response programmatically, checking for brand mentions, sentiment, positioning context, and competitor presence.

## Turning responses into a score

The raw data from 250+ queries is a mess of natural language. Turning it into a single number required a scoring framework that's both granular and honest.

Each response is evaluated on multiple dimensions. Was the brand mentioned at all? Was it mentioned first, or buried at the end of a list? Was the description accurate? Was it framed positively, neutrally, or negatively? Was a competitor recommended instead?

These dimensions feed into a weighted formula. Mention presence is the foundation: if the AI doesn't know you exist, nothing else matters. Positioning (first vs. fifth in a list) matters next. Accuracy and sentiment are modifiers on top.

The final score is normalized to 0-100. From the reports we've run so far, the average business scores around 31. Businesses that have actively worked on their AI visibility can reach 80+. The gap between 31 and 80 is where the action plan comes in. Every report includes prioritized recommendations for closing that gap.

## What we learned building this

**Prompt phrasing changes everything.** Small variations in how you phrase a query produce completely different results. "Best CRM for startups" and "top CRM tools for early-stage companies" sometimes surface different brands on the same engine. Our prompt set is deliberately diverse to smooth out this variance.

**AI engines disagree more than you'd expect.** We regularly see 30+ point score differences between engines for the same brand. A brand might be the default recommendation on ChatGPT and completely absent from Gemini. This isn't a flaw in our scoring. It's a real feature of the current AI landscape, and it matters because your customers use different tools.

**Recency matters, but not equally.** Perplexity and Grok update faster than the others. Brands that recently published strong content see it reflected on Perplexity within days, while Claude and Gemini might lag by weeks or months.

**The action plan is the hard part.** Scoring is solvable engineering. The harder problem is turning "your brand scores 28 on Claude for comparison queries" into concrete next steps. We map each low-scoring area to specific fixes tied to how each engine sources its information, not generic "create more content" advice.

## Where we are now

[Be Recommended](https://berecommended.com) is live and generating reports. The scoring pipeline runs against all five engines for every report. We're continuing to refine the prompt set based on what we see in the data. Some prompt clusters turn out to be more diagnostic than others, and we prune and add based on signal quality.

The average score of 31 tells us something about the market: most businesses haven't thought about AI visibility at all. The ones that have are pulling ahead, because the AI engines are still forming their opinions about most brands. Right now is the window where deliberate work on AI visibility produces outsized results.

If you want to see where your brand stands: [berecommended.com](https://berecommended.com).

---

*Be Recommended is built by [Inithouse](https://inithouse.com), a studio shipping AI-powered products.*
