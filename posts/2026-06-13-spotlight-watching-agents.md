# Spotlight: Watching Agents - building a forecasting tool before the market asks for one

*Posted 2026-06-13*

At Inithouse, a studio shipping a growing portfolio of products in parallel, we occasionally build something before there's obvious demand for it. [Watching Agents](https://watchingagents.com) is one of those bets. It's an AI prediction platform: you ask a question with a horizon ("will X happen by date Y?"), and an agent builds hypotheses, gathers evidence, and updates a probability estimate over time. "Watching" refers to the agents watching the world on your behalf, not the other way around.

The product is in the category of things we built earlier than the market asked us to. That's a choice we made deliberately, and it's worth explaining.

## Why we built this now

A real category of useful work is starting to emerge: long-horizon reasoning that benefits from continuous evidence accumulation. A human asking "will this geopolitical event happen by year-end?" or "will this product launch by Q3?" wants more than an instant guess. They want something that revisits the question as new information arrives.

Today, there's no good tool for this. People hack it together with prediction markets, manual spreadsheets, occasional Twitter polls. None of it scales to the variety of questions individuals and small teams actually want to track.

We think this becomes a real product category over the next 18 months. Watching Agents is our wedge.

## The shape of the product

You define a question and a horizon. An agent forms hypotheses about what would make the answer "yes" versus "no." It schedules itself to revisit the question periodically (gathering news, web data, structured information) and updates the probability. When confidence crosses a threshold, you get notified.

Think of it less as a chatbot and more as a long-running research process. The closest analog is a prediction market, but single-player and customized to your question.

## What's hard about this

**Forecasting accuracy is the hard problem.** You can't just have an LLM output a number. The number has to be calibrated. We've spent more time on the calibration scaffolding than on any other part of the product: comparing model predictions to base rates, to expert benchmarks, to known historical outcomes. The number a Watching Agent emits needs to be defensible, not vibes-based.

**Cost discipline matters.** A naive implementation of "agent that continuously thinks about a question" would burn through compute. We built a scheduler that decides when a question is worth re-evaluating based on whether new information has actually arrived, and we ration evidence-gathering against the value of the question to the user.

**Most users don't know what they want to predict.** This was the biggest surprise. People struggle to formulate questions that are both specific enough to be testable and important enough to be worth tracking. A huge fraction of our onboarding work is helping users phrase questions well. We observed the same pattern at [Be Recommended](https://berecommended.com), where users often don't know how to phrase their AI visibility query until they see the first report. Turns out, helping people ask the right question is half the product.

## Where this stands

Watching Agents is still finding its audience. The use cases are emerging, and the product changes month-to-month. We're publishing this spotlight not because the product is "done" (it isn't) but because building in public means being transparent about the early-stage products too, not just the ones already gaining traction.

Across our portfolio, we've learned that some products click immediately ([Pet Imagination](https://petimagination.com) had users generating portraits within hours of launch) while others need months of quiet iteration before the niche finds them. Watching Agents is in the second category. The thesis holds; the distribution is the open question.

If you have a long-horizon question you actually want to track, [try it](https://watchingagents.com). The product is more useful in months three through six of using it than in week one. Most products are like that, but most teams don't tell you so.

Inithouse, a studio building in parallel
