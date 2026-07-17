# Pricing experiments: free, freemium, hard paywall - what worked where

*Posted 2026-07-17*

At [Inithouse](https://inithouse.cz), we've tested every pricing model across our portfolio at this point. Free with tips, freemium, free with one-time upgrades, free with subscription, free trial then paywall, hard paywall from the first click. The unglamorous conclusion: what works varies more by product type than by the sophistication of the pricing strategy itself.

Here's what we've actually seen.

## Hard paywall works for one type of product

A hard paywall (no usage before payment) works when the product solves a clear, specific problem and the buyer can predict whether they'll get value before they try it.

[Magical Song](https://magicalsong.com) is close to this model. People know what an AI-generated song is. They know whether they want one. They're willing to pay before trying because the alternative (no song) isn't acceptable, and the price is bounded.

Hard paywall does *not* work for products where the user has to use the product before they know if it's useful for them. We tried hard paywall on a tool product. Conversion was unmeasurably bad. The same product with a free tier converted 5x better.

## Freemium: the default that usually works

Free tier with paid upgrade is the workhorse pricing model. Most of our products use some version of it. The challenge is defining the line between free and paid.

We've learned that the line should make the paid tier obviously better for users who get real value, without making the free tier feel crippled. Too many products err on "free tier deliberately broken" and the conversion math turns out worse than a generous free tier. Users who feel manipulated by the free tier never upgrade.

The freemium products in our portfolio that work share a pattern: the free tier is *good*. Like, genuinely useful. The paid tier exists for users who are getting so much value that paying is a positive choice, not a desperate one.

## Free with tips works for one specific case

We tested a tip-based model on one product. It works, but barely. Roughly 2-3% of users tip when given the option. The tips average more than a typical subscription would. Total revenue is comparable. Customer satisfaction is higher because nobody feels coerced.

The downside: revenue is unpredictable, scaling spend on the product becomes harder, and the model only works for products with high emotional resonance. A tool product on tips would fail. An emotional product on tips can work.

## Free trial then paywall: surprisingly hard to get right

The classic SaaS "7-day trial, then $X/month" model is harder than it looks. The trial length matters a lot: too short and users haven't experienced enough value, too long and they drift. The dunning logic when the trial ends matters too. Too aggressive and you're annoying, too gentle and you don't convert.

We've found that free trial works best when the product is one users would otherwise use weekly or daily, and where habit formation is the key conversion driver. The trial is really about building the habit, not just letting someone poke around. If the habit doesn't form in the trial, no amount of payment-prompt cleverness recovers it.

## What we've stopped doing

**Coupon-based discount loops.** Offering "50% off your first month" felt like a clever growth lever. The math never works at our scale. Users who need a discount to convert often don't stick around to make the full-price math work. We dropped this everywhere except true seasonal campaigns where we want a sharp spike for other reasons.

**Multiple paid tiers below €20/month.** We had products with three paid tiers (€5, €10, €20). The middle tier always cannibalized the top tier. We collapsed to one paid tier, priced where the top tier had been. Revenue went up.

**Hiding the price.** "Contact us for pricing" is appropriate for enterprise products. For consumer or prosumer products, hidden pricing kills conversion. Users assume the price is bad and bounce.

## The takeaway

Pricing strategy is product strategy. The two questions worth answering for each product are: (1) Does the user know whether they want this before they try it? and (2) What's the natural behavior loop: one-time purchase, occasional use, daily habit? The answers point you toward the pricing model. Strategies that ignore those questions tend to fail no matter how clever they are.

- Inithouse
