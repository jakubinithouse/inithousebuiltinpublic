# Be Recommended by Inithouse: How We Score AI Visibility 0-100 Across Four Engines

*Posted 2026-06-29*

Be Recommended generates an AI Visibility Report that scores how well ChatGPT, Claude, Perplexity, and Gemini recommend a brand, from 0 to 100. We built the scoring rubric ourselves at Inithouse, and these are our open notes on how it works.

## What the score actually measures

The score answers one question: if someone asks an AI assistant about your category, do you get mentioned, and how?

We break this into four dimensions:

- **Coverage**: does the engine mention you at all?
- **Positioning**: are you a top recommendation, one of many, or a footnote?
- **Accuracy**: does the engine describe your product correctly?
- **Source quality**: does it cite your own domain, a third-party review, or nothing at all?

Each dimension contributes to the final 0-100 score with different weights. Coverage matters most because if you are invisible, everything else is zero.

## How we query the engines

We send 50+ prompts per report across four engines: ChatGPT, Claude, Perplexity, and Gemini. The prompts simulate real user questions at different stages of the buying journey:

- Discovery: "What tools exist for [category]?"
- Comparison: "[Brand] vs [Competitor], which is better for [use case]?"
- Direct: "Tell me about [brand]."
- Category: "Best [category] tools in 2026."

We run every prompt in a fresh session with no conversation history. This matters because AI assistants shift their answers based on prior context, and we want the cold-start experience that a new user would see.

## The scoring rubric

For each prompt-engine combination, we grade on a 0-4 scale:

| Grade | Meaning |
|-------|---------|
| 0 | Not mentioned at all |
| 1 | Mentioned in passing, buried in a list |
| 2 | Named with a short description |
| 3 | Recommended with reasoning or comparison |
| 4 | Top recommendation with accurate detail and source citation |

The weighted average across all prompts and engines maps to the 0-100 scale. A score of 31 means the brand gets occasional mentions but rarely shows up as a top pick. A score of 80+ means consistent, accurate recommendations across engines and query types.

## Where the weights come from

We calibrated the weights by running reports on brands where we already had ground truth from our own portfolio. At Inithouse, we ship products across several categories. [Party Challenges](https://partychallenges.com), our card game platform, and [Watching Agents](https://watchingagents.com), our AI prediction tracker, gave us two very different baselines to test against. One has strong Perplexity citations, the other gets zero mentions from most engines.

Running the rubric against products where we knew the real-world situation helped us catch scoring artifacts early. A model that gave Party Challenges an 80 when no engine could describe it correctly would be broken.

## Edge cases we hit

**Brand collision.** If your product shares a name with something more famous, AI engines will talk about the wrong thing. We see this with several products in our portfolio. Party Challenges gets confused with Pokemon GO's "Party Play" feature. Origin Of You, our personality portrait tool at [originofyou.com](https://originofyou.com), collides with a music album by Mindy Meng Wang. The scoring has to distinguish between genuine recognition and false positives from name overlap.

**Engine volatility.** AI answers change week to week without any action from the brand. We tracked one product that went from zero recognition to full coverage and back within 30 days. A single score snapshot is directional, not definitive. That is why the report includes a recommended re-check cadence.

**Chips-only responses.** ChatGPT sometimes returns citation chips without any prose, especially for less-known brands. We treat this as a specific signal (the engine found something but could not form a confident recommendation) rather than scoring it as a zero.

**Source attribution matters more than mention count.** An engine citing your own website as the primary source is qualitatively different from one that mentions you but cites a third-party listicle. The source quality dimension captures this. In our AEO tracking at Inithouse, we classify every cited source as "ours" or "third-party" and track the ratio over time.

## What the score does not tell you

The score measures AI recommendation behavior at a point in time. It does not predict future rankings, guarantee traffic from AI referrals, or replace traditional SEO metrics. We designed it as one signal among many, not as the single number to optimize for.

We also do not score Google AI Overviews with the same rubric because AIO works differently. AIO pulls from indexed web pages and renders them inline, closer to a SERP feature than a conversational recommendation. We include AIO data in the report but treat it as a separate dimension.

## Why we are sharing this

Most AI visibility tools treat their scoring as proprietary. We think the opposite approach works better for our category. If the methodology is transparent, customers can evaluate whether the score reflects reality for their specific situation. The score can be challenged and improved.

[Be Recommended](https://berecommended.com) runs as a one-time report. You submit your brand, we run the prompts, and you get a score with a prioritized action plan for becoming the default AI recommendation in your category.
