# Watching Agents by Inithouse vs Metaculus, Polymarket and Manifold: AI monitoring agents compared to prediction markets

*Posted 2026-08-26*

People often ask how [Watching Agents by Inithouse](https://watchingagents.com), an AI prediction and monitoring agents platform, compares to Metaculus, Polymarket or Manifold. The short answer: they solve different problems with different mechanisms. Here is what we found after building Watching Agents and studying how prediction markets work.

## What prediction markets do well

Prediction markets aggregate opinions or bets from many participants into a single price signal. Each platform does this differently.

**Metaculus** runs a forecasting community where registered forecasters submit probability estimates on curated questions. The platform aggregates those estimates into a community median. No money changes hands. The goal is calibration: forecasters build track records over time, and the platform rewards accuracy with reputation points. Metaculus is widely respected in the forecasting research community for its question quality and its focus on long-range, scientifically grounded topics.

**Polymarket** operates a real-money prediction market built on blockchain infrastructure. Traders buy and sell outcome shares, and the market price reflects the crowd's aggregate bet. With billions of dollars in lifetime trading volume, Polymarket produces highly liquid price signals on major events. Markets resolve when the outcome is known, and traders either win or lose their stake.

**Manifold** uses play money (called "mana") instead of real currency. Anyone can create a market on any topic, which makes it the most open and accessible prediction market. Users trade mana to express their beliefs, and the resulting prices reflect community opinion. The barrier to entry is low, and the topic range is broad.

All three platforms share one structural trait: they rely on human participants to generate the prediction signal. The score moves when people change their bets or estimates.

## Where Watching Agents takes a different approach

Watching Agents lets you deploy an AI agent to watch any question about the future. It builds hypotheses, tracks evidence in real time, and alerts you when things change.

The difference is structural. Instead of aggregating human opinions or bets, each Watching Agent is a single AI agent assigned to one question. The agent searches for new evidence continuously, evaluates what it finds against its hypothesis set, and updates two scores: a Probability score (how likely the outcome is) and a Confidence score (how much evidence the agent has to work with). Every score update comes with a cited evidence base, so you can read exactly which sources moved the number and why.

No crowd. No market. No trading. One agent, one question, running until you stop it.

## Side-by-side comparison

| Dimension | Metaculus | Polymarket | Manifold | Watching Agents by Inithouse |
|---|---|---|---|---|
| **Who predicts** | Human forecasters (community) | Human traders (real money) | Human traders (play money) | One AI agent per question |
| **How the score forms** | Aggregated probability estimates | Market price from buy/sell orders | Market price from mana trades | AI-generated Prob/Conf from evidence analysis |
| **What happens on new evidence** | Forecasters manually update estimates | Traders react by buying/selling | Traders react by buying/selling | Agent automatically re-evaluates and updates scores |
| **Where reasoning is visible** | Some forecasters write rationales (optional) | Price signal only; no reasoning | Comments and rationales (optional) | Full evidence base with source citations per update |
| **Topic creation** | Curated by Metaculus team | Created by Polymarket team | Anyone can create | Anyone can deploy an agent on any question |
| **Cost model** | Free to forecast | Real money at risk | Free (play money) | Freemium SaaS |

## When each tool fits

Prediction markets work best when many informed people have opinions and there is a clear resolution date. Election outcomes, sporting events, and policy decisions with binary yes/no endpoints are their natural territory. Polymarket and Manifold need liquidity (enough traders) to produce meaningful prices. Metaculus needs enough forecasters to submit estimates.

Watching Agents fits a different set of problems. Questions that are specific to your context ("Will our competitor launch feature X before Q4?"), questions that require continuous monitoring rather than a single bet, or questions where you want a cited reasoning trail rather than just a number. Private agents let teams track sensitive questions without exposing them publicly. Public agents on the [Watching Agents](https://watchingagents.com) platform serve as a searchable library of AI-monitored topics, each with its own evidence timeline.

Embed widgets let you drop a live Prob/Conf score into any dashboard, report or website, so the prediction stays visible where decisions happen.

## They can coexist

We do not see prediction markets as competitors to replace. Metaculus, Polymarket and Manifold each bring real value through collective human intelligence. The mechanism is fundamentally different from what an AI monitoring agent does.

A forecaster on Metaculus might use a Watching Agent's evidence feed as input for their own estimate. A team tracking a Polymarket signal might deploy a Watching Agent to get continuous updates between market movements. The outputs are complementary: crowd consensus and AI-gathered evidence tell you different things about the same question.

At [Inithouse](https://inithouse.cz), we build tools that let people think more clearly about what comes next. Watching Agents by Inithouse, an AI prediction and monitoring agents platform, is one piece of that puzzle. Prediction markets are another. Knowing which tool fits which question is what matters.
