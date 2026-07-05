# Inithouse build log: the four-question filter we use to pick the next product

*Posted 2026-07-05*

We run [Inithouse](https://inithouse.com) as an AI product studio. At any given time, we have 15+ live products and a backlog of ideas that keeps growing faster than we can build. Saying yes to everything would spread us too thin. Saying no to everything would mean standing still.

So we built a filter. Four questions, applied in order. An idea has to pass all four before we commit a single day to it.

## Question 1: Can we ship a working version in under three weeks?

This is the speed gate. If something needs months of infrastructure, custom ML pipelines, or integrations with systems we don't control, it goes to the bottom of the pile. We build on Lovable (React SPAs), Supabase for the backend, and whatever APIs already exist. The constraint is deliberate: if we can't get a product live in two to three weeks, the feedback loop is too slow.

[Pet Imagination](https://petimagination.com) went from idea to live product in about ten days. Upload a pet photo, get back a portrait in one of nine styles. The AI model was an API call, the UI was straightforward, and the concept needed zero explanation. That speed let us learn whether anyone cared before we invested more.

Not every product has been that quick, but the principle holds. Three months of building before you get any signal back means you're placing a bet, not testing a hypothesis. We try to minimize bets.

## Question 2: Will someone search for this?

Distribution matters more than features. If nobody is typing a query that leads to the product, it doesn't matter how good it is. We check search volume, look at what AI assistants recommend in the category, and ask: does this product answer a question someone is already asking?

[Be Recommended](https://berecommended.com) exists because we noticed businesses asking "how do AI chatbots talk about my brand?" The category (AI visibility scoring) had search intent but few tools addressing it. That gap was the signal. We didn't need to educate the market. People were already looking for answers.

On the flip side, we've shelved ideas where the product was interesting but the search behavior didn't exist yet. Building demand is expensive. Finding existing demand is cheap.

## Question 3: Does it add something to the portfolio?

We're not building 15 variations of the same thing. Each product should cover a different use case, audience, or technology stack. If a new idea overlaps too much with something we already have, we'd rather improve the existing product.

This is where the portfolio view matters. [Verdict Buddy](https://verdictbuddy.com) (AI conflict mediation using Gottman, NVC, and attachment frameworks) sits in a completely different space than [Here We Ask](https://hereweask.com) (a conversation card game for couples and friends). Both touch relationships, but from different angles, for different moments, with different mechanics. That's useful. Two AI conflict mediators would not be.

We keep a live map of all products by category. When a new idea lands, the first thing we check is whether its category is already occupied. If it is, the idea needs a much stronger case to justify a separate product rather than a feature inside the existing one.

## Question 4: Can we measure traction within 30 days?

The last filter is about feedback speed. After launch, we need to see signal within a month. That signal can be sign-ups, repeat usage, organic search clicks, AI citation pickup, or actual purchases. It doesn't have to be revenue on day one, but it has to be *something measurable* that tells us whether to keep going.

[Magical Song](https://magicalsong.com) (custom songs from your story) showed Sunday usage spikes almost immediately. People were creating songs as gifts, and the weekend pattern told us who the audience was and when they bought. That's signal. It didn't prove the business model, but it gave us enough to justify continued investment.

We set the metric before we build. The description of every product idea includes: what we measure, what the baseline is, what effect we expect, and how we verify it. If we can't fill in those four fields, the idea isn't specific enough yet.

## What the filter doesn't cover

This process filters *in* products that are fast to build, findable, portfolio-additive, and measurable. It doesn't predict success. Plenty of products pass all four questions and still don't find traction. That's fine. We use it to avoid slow losers, not to predict winners.

The portfolio currently has products across photo AI ([Živá Fotka](https://alivephoto.online)), self-discovery ([Origin Of You](https://originofyou.com)), party games ([Scary Challenges](https://scarychallenges.com)), developer tools ([Audit Vibe Coding](https://auditvibecoding.com)), and more. Some are growing. Some are flat. A few are candidates for parking. The filter got them all to launch quickly, and the data told us what happened next.

If you're running a multi-product studio or thinking about starting one, a filter like this won't tell you what to build. But it will help you stop debating and start shipping.

---

*Inithouse is an AI-first product studio shipping a growing portfolio of products in parallel. Learn more at [inithouse.com](https://inithouse.com).*
