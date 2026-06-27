# The metric we ignored for too long

*Posted 2026-06-27*

Every studio has a story about a metric they finally started tracking and wish they'd tracked from day one. Ours is "time to first value."

For most of our portfolio's history, we measured the obvious things: visitors, signups, conversions, revenue. Those are the metrics every analytics dashboard puts in front of you. They are also, in retrospect, lagging indicators of a problem we'd been failing to notice for two years.

The problem: across most of our products, the gap between "someone signs up" and "someone gets something useful out of the product" was too long. People signed up. People didn't come back. We assumed the problem was retention. The problem was that they never reached the first moment of value.

## What "time to first value" means in practice

It's the actual elapsed time, in seconds or minutes, between a user's first interaction with the product and the moment the product has done something useful for them.

For [Magical Song](https://magicalsong.com), this is the moment the user hears the preview of their custom song. Time matters here because the emotional momentum dies if you make people wait too long.

For [Pet Imagination](https://petimagination.com), it's the moment of seeing the first portrait preview. Same logic.

For [Verdict Buddy](https://verdictbuddy.com), it's getting the first verdict back. Should be near-instant, often wasn't, because we'd added too much friction before the verdict screen.

For [Be Recommended](https://berecommended.com), it's the moment a user sees the first piece of data about their own product's visibility. Originally this took five minutes of setup. Now it takes thirty seconds.

## What we did

We instrumented every product to log the timestamps at each step of the onboarding-to-first-value flow. We ran the math. Across the portfolio, the median time to first value for new signups was *much* longer than we'd have guessed. Several products were five-plus minutes. One was over fifteen.

Then we ran the corresponding cohort analysis. Users who reached first value in under 60 seconds had vastly better day-7 retention than users who took two minutes. Users who took two minutes had vastly better retention than users who took five. The curve fell off a cliff somewhere around the three-minute mark for most products.

We didn't have a retention problem. We had a "users never reached the first useful moment" problem.

## What we changed

The interventions were boring. Cut steps from onboarding. Pre-fill defaults. Skip "select your preferences" screens entirely and infer preferences from behavior. Move the first useful output earlier in the flow. Show preview content before login, not after. Make the demo data look like the user's actual likely data, not generic placeholder data.

Each change was small. The cumulative effect was that median time to first value across the portfolio dropped to under 90 seconds. Retention metrics improved correspondingly.

## Why this took us two years

A few reasons, none flattering.

**The metric isn't on standard dashboards.** Google Analytics doesn't show you time-to-first-value because it doesn't know what "value" means for your product. You have to define it, instrument it, and watch it yourself. We hadn't.

**It's not the same thing as conversion.** Conversion rate is a sieve. It tells you how many people got through. Time-to-first-value tells you why most of the others didn't.

**We were optimizing the wrong end of the funnel.** We spent a long time iterating on landing pages and ad copy when the bigger leak was in onboarding. The data was telling us where the leak was; we weren't asking the right question of the data.

## The takeaway

If you have a product where users sign up and most never come back, instrument the time-to-first-value first. Before you redesign anything. Before you A/B test anything. Just measure how long it takes someone new to actually get something out of your product. The answer will probably surprise you.

*[Inithouse](https://inithouse.com) is a small studio running a portfolio of MVPs in search of product-market fit.*
