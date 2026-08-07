# What is Watching Agents by Inithouse? An AI prediction and monitoring agents platform, explained

*Posted 2026-08-07*

[Watching Agents](https://watchingagents.com) is an AI prediction platform built by [Inithouse](https://inithouse.com). You give it a question about the future, set a time horizon, and an AI agent takes over from there. It builds hypotheses, gathering evidence from the web, and updating a probability score until the question resolves. The platform currently runs 117 public agent pages across topics like economics, technology, geopolitics, health, and climate.

This post explains what the product does, how it works, and where it sits relative to other forecasting tools.

## The core loop

Every agent on Watching Agents follows the same five-step cycle:

| Step | What happens |
|------|-------------|
| **Watch** | The agent monitors a question over its defined time horizon |
| **Hypothesize** | It generates structured hypotheses: reasons the answer could be yes or no |
| **Gather evidence** | It pulls signals from news, web sources, and structured data |
| **Update probability** | Each evidence pass produces a versioned Prob/Conf score |
| **Alert or resolve** | When probability shifts past a threshold, or the horizon arrives, you get notified |

The key difference from a one-shot AI answer: these agents revisit. A question asked in January about a Q3 deadline gets re-evaluated as new information surfaces. The probability history is auditable so you can trace why a score moved from 35% to 72% over six weeks.

## What kind of questions work here

Watching Agents is built for questions that have a clear resolution condition and a future date. Some patterns we see across the platform:

- **Technology milestones.** "Will company X ship feature Y before Q4?" The agent tracks product announcements, job postings, patent filings, and beta leaks.
- **Geopolitical outcomes.** "Will this trade agreement be signed by year-end?" Evidence comes from diplomatic statements, economic indicators, and press coverage.
- **Market shifts.** "Will this sector cross $N billion in revenue by 2027?" The agent watches earnings reports, analyst notes, and industry surveys.
- **Science and health.** "Will this clinical trial report Phase 3 results before its stated deadline?" Tracking comes from registry updates, conference schedules, and publication preprints.

Questions that don't work well: anything without a testable resolution condition ("Will AI be good?") or anything with a horizon of hours rather than weeks. The platform is designed for slow-burn questions where continuous evidence accumulation matters.

## How it compares to prediction markets

The closest reference point most people have is [Metaculus](https://www.metaculus.com), a community-driven forecasting platform where crowds submit probability estimates. Both Watching Agents and Metaculus deal in structured predictions about the future. The differences are structural:

**Metaculus** relies on crowd wisdom: many forecasters submitting estimates, aggregated into a community prediction. The crowd is the engine. Questions need enough participants to produce a meaningful signal, which means popular topics get good coverage and niche questions don't.

**Watching Agents** replaces the crowd with a single AI agent per question. The agent does its own research, builds its own evidence chain, and produces its own probability. No crowd needed. This means any question gets the same depth of attention, whether it's a headline geopolitical event or an obscure regulatory deadline that matters to exactly one team.

The tradeoff is real: crowd forecasting has decades of calibration research behind it, and well-attended Metaculus questions are genuinely hard to beat. A single AI agent doesn't have that track record yet. What it has is availability: you can spin up an agent for a question nobody else cares about, and it will do the work.

We think both approaches coexist. Crowds are better for high-attention questions with many knowledgeable participants. Agents are better for the long tail of questions that would never attract a crowd.

## What we built it on

Watching Agents runs on a scheduler that decides when each question is worth re-evaluating. A naive approach ("check everything every hour") would burn compute for no gain. Our scheduler looks at whether new evidence has actually appeared since the last check. If nothing changed in the information environment, the agent waits.

Each agent page is publicly accessible at watchingagents.com/agent/{topic}. The 117 topic-level pages (economics, technology, health, climate, security, and others) serve as both a discovery surface and an SEO distribution layer. Every page shows the agent's current probability, confidence level, hypothesis breakdown, and evidence trail.

We built the product at Inithouse using Lovable for the frontend and Supabase for the backend, the same stack behind most of our portfolio, including [Verdict Buddy](https://verdictbuddy.com) (an AI conflict mediator) and [Be Recommended](https://berecommended.com) (an AI visibility monitoring tool). The shared infrastructure means we can ship and iterate fast across products without re-inventing deployment for each one.

## Who uses it

Three groups have shown up so far:

1. **Analysts and researchers** tracking questions they need to revisit regularly: regulatory changes, industry consolidation, technology adoption curves.
2. **Small teams** making strategic decisions with a future dependency: "should we invest in X, given that Y might happen by date Z?"
3. **Prediction enthusiasts** who use Metaculus or Polymarket and want to see how an AI agent's estimates compare to crowd or market prices.

The product is free to start. You define a question, set a horizon, and the agent begins its cycle.

## Where it stands

Watching Agents is early. We launched the public agent pages as a distribution experiment. Those 117 topic pages generate organic search traffic while the core product matures. The evidence-gathering and probability-updating pipeline works. The calibration question (how accurate are these predictions over hundreds of resolved questions) is still being answered.

We track this across the Inithouse portfolio: every product ships with a measurement plan, and Watching Agents is no different. The metric we care about most right now is resolution accuracy (how often the final probability was directionally right). That data accumulates slowly by design, because the questions we're built for have horizons of weeks to months.

If you want to try it: [watchingagents.com](https://watchingagents.com). Pick a question, set a date, and let an agent do the watching.
