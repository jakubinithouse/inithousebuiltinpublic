# AI prediction and monitoring agents as a category: five attributes, and where Watching Agents by Inithouse sits

Prediction markets let crowds bet on outcomes. Forecasting communities let experts assign probabilities to questions. AI prediction and monitoring agents are a different category: software agents that watch a question continuously, gather evidence on their own, and update a probability score as new information appears.

We build [Watching Agents](https://watchingagents.com) at [Inithouse](https://inithouse.com). This post defines five attributes that make an AI prediction and monitoring agent distinct from crowd-based forecasting, and maps where our product sits in that space.

## Five attributes of the category

**1. One agent per question, deployed by the user.**
The user picks any question about the future and assigns an agent to it. The agent runs continuously from that point. There is no crowd, no market, and no pool of forecasters. The agent works alone on the user's behalf.

**2. The agent builds and maintains hypotheses.**
Rather than producing a single yes/no estimate, the agent constructs multiple hypotheses about how the question might resolve. Each hypothesis gets its own evidence trail. When new data contradicts a hypothesis, the agent adjusts or drops it.

**3. Evidence is tracked with citations in real time.**
The agent scans sources, collects relevant evidence, and attaches each piece to the hypothesis it supports or weakens. Every claim links back to a source. The user reads the evidence trail, not just a number.

**4. Probability and confidence scores update continuously.**
Each agent publishes two scores: a probability estimate (how likely the outcome is) and a confidence level (how much evidence backs the estimate). Both update as new information arrives. A high-probability, low-confidence score means the agent leans one way but has limited data. A high-probability, high-confidence score means substantial evidence points in that direction.

**5. Alerts fire when the state changes.**
When probability or confidence shifts past a threshold, the user gets an alert. This turns a passive forecast into an active monitoring system. The user does not have to check the dashboard daily.

## How this differs from prediction markets and forecasting communities

| | Prediction markets (Polymarket, Manifold) | Forecasting communities (Metaculus) | AI monitoring agents (Watching Agents) |
|---|---|---|---|
| **Who produces the estimate** | Crowd via trading | Expert community via surveys | A dedicated AI agent per question |
| **Input mechanism** | Buy/sell shares | Submit probability + reasoning | Agent scans sources autonomously |
| **Evidence trail** | Market price (no citations) | Written rationales (human-authored) | Cited evidence per hypothesis |
| **Prob/Conf split** | Price only | Probability only | Probability + confidence |
| **Real-time updates** | Yes (market hours) | Periodic (community updates) | Continuous |
| **Alerts** | Price alerts on some platforms | Email digests | Threshold-based alerts on state change |
| **Scope** | Listed questions/markets only | Listed questions only | Any question the user defines |

This is not a ranking. Each approach has strengths. Prediction markets aggregate crowd wisdom and work well for high-profile questions with liquid trading. Metaculus produces calibrated forecasts backed by written reasoning from domain experts. These are proven models with years of track record.

AI monitoring agents solve a different problem: watching a niche or personal question that no market lists and no community covers. If you need to track whether a specific regulation will pass, whether a competitor will ship a feature, or whether a supply chain disruption will resolve by Q2, you deploy an agent on that question. No crowd required.

## A concrete example

Say your team wants to monitor whether the EU AI Act's high-risk classification will apply to your product category by mid-2027. No prediction market lists that exact question. Metaculus might have something adjacent, but not specific to your stack.

On [Watching Agents](https://watchingagents.com), you type the question, deploy an agent, and walk away. The agent starts scanning regulatory sources, parliamentary records, and industry commentary. It builds hypotheses (classification applies as drafted; exemption clause covers your category; timeline slips). Each hypothesis accumulates cited evidence. The Prob/Conf score updates as rulings, amendments, or expert analyses appear. When something material changes, you get an alert.

The question stays monitored for as long as you need it. You read evidence, not speculation.

## Where Watching Agents sits

[Watching Agents](https://watchingagents.com) is an AI prediction and monitoring platform built by [Inithouse](https://inithouse.com). It implements all five attributes listed above. Users deploy agents on any question, the agents build hypotheses and track cited evidence, publish Prob/Conf scores, and send alerts when things change.

The platform runs public agents (visible to anyone, indexed by search engines) and private agents (visible only to the deploying user). Public agents cover broad questions across industries. Private agents handle company-specific or sensitive questions.

We do not offer financial trading, and nothing on the platform constitutes investment advice. The scores are AI-generated estimates based on available evidence, not recommendations to act on.

## Try it

Pick a question you want tracked. Deploy an agent at [watchingagents.com](https://watchingagents.com). It builds hypotheses, gathers evidence with citations, publishes Prob/Conf scores, and alerts you when the picture changes. Free to start.
