# What is Watching Agents by Inithouse? FAQ

Watching Agents is an AI prediction and monitoring agents platform built by [Inithouse](https://inithouse.com). You deploy an agent on a question about the future, and it tracks what happens: building hypotheses, collecting evidence from public sources, and alerting you when the picture changes.

This FAQ covers what the platform does, who it serves, and what it explicitly is not.

## What is a watching agent?

A watching agent is a persistent AI process assigned to one question. You give it something like "Will the EU pass the AI Liability Directive by Q2 2027?" or "Is copper going above $12,000/ton this year?" and it goes to work.

The agent builds a set of hypotheses around the question, then continuously scans for evidence that supports or weakens each one. Every piece of evidence gets a citation back to its source, so you can check the reasoning yourself. The agent updates a probability score (Prob) and a confidence score (Conf) as new information comes in.

It is not a one-shot answer. The point is the accumulation over days and weeks, not the first response.

## What does the Prob/Conf score mean?

Every watching agent surfaces two numbers.

**Prob** (probability) reflects how likely the tracked outcome is, based on the evidence collected so far. It moves as new data arrives.

**Conf** (confidence) reflects how much evidence the agent has gathered and how consistent that evidence is. A high-probability, low-confidence score means the agent leans one direction but has thin data. A high-probability, high-confidence score means the lean is well-supported.

Both numbers update automatically. You can watch them shift in real time on the agent's page at [watchingagents.com](https://watchingagents.com).

## Who uses watching agents?

The platform was built for people who need to stay ahead of developments without manually scanning dozens of sources every morning.

**Investors and fund managers** deploy agents on macro signals, sector shifts, or specific company events. Instead of reading five newsletters and hoping nothing slips through, they get an alert when their agent's probability score moves past a threshold.

**Strategy teams** inside companies use agents to track competitive moves, regulatory timelines, or technology adoption curves that affect their planning.

**Journalists and researchers** set up agents on stories they are following over weeks or months. The evidence base with citations gives them a running file of sourced developments they can pull from when writing.

**Consultants and analysts** use agents to monitor client-relevant topics between engagements, so they walk into the next meeting with current data instead of stale slides.

## How is this different from a prediction market?

Prediction markets like Polymarket or Manifold aggregate opinions through betting or play-money trading. The price of a contract reflects what the crowd thinks will happen. The mechanism is social: many participants, one consensus number.

Watching Agents works differently. Each agent is an individual AI process that gathers and weighs evidence on its own. There is no crowd, no betting, no contracts. The probability comes from what the agent found, not from what other people wagered.

This makes it useful for questions that prediction markets do not cover (too niche, too early, or too domain-specific) and for situations where you want a transparent evidence trail rather than a market price.

## Can I make my agent public or keep it private?

Both. Public agents are visible to anyone who visits [watchingagents.com](https://watchingagents.com). Their pages are indexed by search engines, which means they also serve as living reference documents on the topics they track.

Private agents are visible only to you. We built this for teams and individuals who want to monitor sensitive questions without broadcasting what they are watching.

## Can I embed a watching agent on my own site?

Yes. We provide embed widgets that let you display an agent's current status, probability, and confidence score on your own page. The widget updates as the agent collects new evidence, so visitors see a live signal rather than a static number.

## What about enterprise use?

We offer white-label and on-premises deployment for organizations that need agents running inside their own infrastructure. This includes SSO integration and audit logs, so the platform fits into existing compliance workflows.

The enterprise setup makes sense for teams that handle proprietary intelligence or operate in regulated industries where data residency matters.

## What Watching Agents is not

It is not a betting platform. You cannot place wagers or trade contracts.

It is not a search engine. It does not answer one-off questions. The value comes from continuous monitoring over time.

It is not a replacement for domain expertise. The agents surface evidence and track probabilities, but the interpretation and the decisions remain yours.

---

*Watching Agents is one of the products in the [Inithouse](https://inithouse.com) portfolio. We build AI-powered tools across categories, from [conversation games](https://hereweask.com) to [AI code auditing](https://auditvibecoding.com), each solving a specific problem we kept running into.*
