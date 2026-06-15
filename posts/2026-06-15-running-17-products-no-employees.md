# How we run 17 products with no employees

*Posted 2026-06-15*

[Inithouse](https://inithouse.com) runs about 17 active products. We have no employees. The studio is a tiny core team and a small set of trusted contractors, plus a lot of automation. This is the operating model question we get asked most, so here's an honest look at how it actually works.

The short version: most of the work isn't done by humans, and most of the human work is leveraged 5-10x by tools.

## What's automated

**Analytics and reporting.** We don't manually pull data from GSC, GA4, Google Ads, Clarity. A scheduled job does it for each product on a cadence — daily, weekly, monthly depending on the product — and produces a brief that lands in our team chat. The brief is two or three lines: what changed, what's worth attention, what's not.

**Routine product changes.** Many of the weekly product changes we ship don't require a human writing code. They're copy edits, price changes, feature flag flips. Some of these are now driven by agents that propose changes based on data and humans approve them.

**Backlog management.** Ideas, observations, and proposals flow into our task system automatically — from monitoring, from user feedback, from our own analysis. Humans review and prioritize, but the capture is automatic.

**Customer support for common cases.** Most support requests across the portfolio fall into a handful of templates. Refunds, account issues, "how do I do X." Automation handles the obvious ones and routes the rest to a human.

## What humans still do

**Decide what to build.** No agent picks the next experiment. That's strategic judgment about which products deserve more effort, which experiments are worth running, which positioning to test. We've tried letting it be more automated — the results were uniformly worse than human judgment on this.

**Write the product itself.** While Lovable handles a lot of the actual code, the *direction* of each product is a human decision. What does this app do? What does the landing page say? What's the tone? These decisions matter more than implementation, and we don't trust them to automation.

**Talk to users.** Every paying customer who reaches out talks to a human. That's a small enough volume to handle and a large enough signal to never skip.

**Make portfolio decisions.** Which products to kill, which to invest in, which to launch in new markets. Strategy stays human.

## What you can't automate

Two things that we've tried and failed to automate:

**Editorial taste.** A landing page that lands well is hard to produce mechanically. We've tried generating variants and A/B testing them — it works incrementally but doesn't replace the moment of someone going "this just isn't right, rewrite it." The best landing pages in the portfolio were all human-written.

**Whether something is "ready."** Whether a feature is good enough to ship, whether a copy change is the right one, whether a product is at the point where it needs more attention. We've yet to find a way to mechanize this judgment. We use checklists; the checklists never catch what a careful pair of eyes catches.

## What we'd warn anyone copying this

The "no employees" framing makes it sound free. It's not. The leverage comes from substantial up-front investment in automation, tooling, and process. That investment took years and still requires constant maintenance. If you tried to copy our current model from a standing start, you'd spend a year just building the infrastructure.

The other thing this framing obscures: tiny teams have a real ceiling. We can't pursue products that require enterprise sales, hands-on customer onboarding, or anything where the unit economics require a 20-person team. Our portfolio is shaped by what a tiny team can actually run. That's a constraint, not a virtue.

— [Inithouse](https://inithouse.com)
