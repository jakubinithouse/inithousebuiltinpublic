# Build log: real-time evidence tracking inside Watching Agents

*Posted 2026-07-04*

When we started building the evidence tracking system for [Watching Agents](https://watchingagents.com) at Inithouse, the first prototype was embarrassingly simple. The agent ran a search once a day, dumped everything it found into a list, and recalculated probabilities. It worked for questions with a six-month horizon. For anything shorter than two weeks, it was useless. By the time the agent noticed a shift, the question had already resolved.

This post is about what we changed to make evidence tracking feel closer to real-time, and the trade-offs we accepted along the way.

## The source graph

Every question in [Watching Agents](https://watchingagents.com) has a source graph. When the agent first processes a question, it identifies the entities involved (companies, people, legislation, scientific concepts) and maps them to a set of source feeds. These are not hardcoded lists. The agent generates them dynamically based on the question text.

For a question about a pending FDA approval, the source graph might include the FDA press release page, the company investor relations feed, ClinicalTrials.gov for that specific drug, and three or four major health news outlets. For a geopolitical question, it skews toward wire services and government press offices.

We store source graphs per question rather than globally because two questions about the same company can need different source mixes. A question about a merger tracks SEC filings and antitrust news. A question about a product launch tracks tech press and patent databases. Same company, different sources.

## Scan scheduling

The original once-a-day scan was the obvious first thing to fix. But scanning everything constantly was not the answer either. We run many agents across many questions, and most sources do not update every hour.

We landed on adaptive scan intervals. Each source in the graph has its own scan frequency, starting at a default of six hours. Two things adjust it.

First, evidence velocity. If a source has produced three relevant pieces of evidence in the past 24 hours, its scan interval drops to one hour. If it has produced nothing relevant in a week, the interval stretches to 24 hours. The adjustment is gradual, not instant, to avoid thrashing on a single busy day.

Second, question urgency. As a question resolution date approaches, all its source intervals tighten. A question resolving in three days gets scanned roughly three times more often than one resolving in three months. The multiplier follows a curve that steepens in the final week.

This adaptive system cut our compute costs by about 60% compared to uniform high-frequency scanning while catching time-sensitive developments faster.

## Evidence deduplication

Real-time tracking creates a deduplication problem. The same news gets reported by twenty outlets within an hour. If the agent logs all twenty as separate evidence, the probability update is wildly overstated because the Bayesian update treats each piece as independent.

We handle this in two stages.

The first stage is URL-level dedup. If two evidence items link to the same canonical URL (after stripping tracking parameters and resolving redirects), they merge. Simple, and catches about 40% of duplicates.

The second stage is semantic dedup. For evidence with different URLs but similar content, the agent computes an embedding of each item summary and clusters anything above a cosine similarity threshold. The cluster becomes a single evidence entry with the highest-authority source as the primary citation and the rest listed as corroborating sources.

This matters more than it sounds. In one early test, a technology question picked up 14 articles about the same announcement in a single scan. Without dedup, the agent would have shifted the hypothesis probability as if it had found 14 independent signals. With dedup, it correctly counted one strong signal from a primary source with 13 corroborations.

## The evidence chain

One of the things that distinguishes [Watching Agents](https://watchingagents.com) from prediction markets like Metaculus or Polymarket is the evidence chain. Every probability update is traceable back to the specific evidence that caused it. You can open any agent page and see not just the current probability but the full timeline of how it got there.

We built the evidence chain as an append-only log. Each entry records the timestamp, the evidence that triggered the update, which hypothesis it affected, the direction (supports or weakens), the old probability, and the new probability. Nothing gets deleted or overwritten.

This design has a practical benefit beyond transparency. When we tune the scoring model, we can replay the evidence chain against a new model and compare outputs. If the new model would have caught a reversal two days earlier, we know the tuning is working. If it would have generated a false alert, we know to back off.

## Handling contradictory evidence

The interesting engineering challenge is when two credible sources disagree within the same scan window. Source A says a deal is likely. Source B says negotiations have stalled. Both are primary sources. Both are recent.

Our approach is to let both pieces of evidence affect the hypotheses and rely on the confidence score to signal ambiguity. When contradictory evidence arrives simultaneously, the probability may stay roughly flat (the signals cancel out), but the confidence score drops. A dropping confidence score tells the user: something is happening, the picture is unclear, pay attention.

We considered fancier approaches like weighted arbitration between sources or sentiment analysis to detect hedging language. We shipped the simple version first. It has been good enough that the fancier approaches keep getting deprioritized.

## Where we are now

The evidence pipeline runs across all public agents on [Watching Agents](https://watchingagents.com). Average latency from a source publishing new content to the agent incorporating it as evidence is about two hours, driven mostly by the adaptive scan interval. For high-velocity questions nearing resolution, that drops to under thirty minutes.

At Inithouse, we have been using the evidence chain internally to spot patterns in how questions resolve. Questions where evidence velocity spikes sharply tend to resolve faster than their original time horizon suggested. Questions where evidence trickles in steadily tend to overshoot their horizon. We are not sure yet what to do with that observation, but it is consistent enough that we are tracking it.

The next piece we are working on is source discovery. Right now, the agent builds its source graph once when the question is created and rarely updates it. Questions that span months sometimes develop new relevant sources midway through. Teaching the agent to expand its own source graph based on evidence patterns is next on the list.
