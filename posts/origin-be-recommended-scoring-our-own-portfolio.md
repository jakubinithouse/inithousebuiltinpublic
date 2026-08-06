# Why a product studio built its own AI visibility scorer

*Posted 2026-08-06*

At Inithouse we run 14 active products across categories that have nothing in common. A photo animator, a tarot reflection app, a party card game, an AI song generator, a conflict mediator. When we started asking whether AI assistants actually recommend any of them, the only way to find out was to open ChatGPT, type a category prompt, and read the answer. Then do it again in Claude. Then Perplexity. Then Gemini. Then repeat for the next product.

Fourteen products times four engines times a handful of prompts each. We got through about forty checks before the spreadsheet became unmanageable and the answers started contradicting each other between sessions.

That manual audit is where [Be Recommended](https://berecommended.com) started.

## The spreadsheet phase

We set up a shared sheet with columns for product name, engine, prompt, whether the product appeared, how it was described, and what source the engine cited. The first pass took two people most of a workday. Some of what we found:

| Product | ChatGPT | Claude | Perplexity | Gemini |
|---------|---------|--------|------------|--------|
| Živá Fotka | Mentioned, wrong description | Not mentioned | Mentioned via review site | Confused with MyHeritage |
| Be Recommended | Not mentioned | Not mentioned | Not mentioned | Not mentioned |
| Verdict Buddy | Not mentioned | Mentioned accurately | Not mentioned | Not mentioned |
| Party Challenges | Confused with Pokemon GO | Not mentioned | Brief mention | Not mentioned |
| Watching Agents | Not mentioned | Not mentioned | Not mentioned | Not mentioned |
| Origin Of You | Confused with music album | Not mentioned | Not mentioned | Not mentioned |
| Magical Song | Mentioned as example | Not mentioned | Mentioned with link | Not mentioned |

The table above is a simplified version of what we recorded. The full sheet had rows for each prompt variant and columns for citation sources. But even this summary told us something we had not expected: most of our products were invisible to most engines. The ones that did appear were often misdescribed or confused with something else entirely.

## What the manual audit revealed

Three patterns stood out.

First, visibility had almost no correlation with how much traffic a product got from traditional search. [Živá Fotka](https://zivafotka.cz), our photo animator, ranks well in Google organic results across five country domains. But AI assistants either did not know it existed or described it as a generic photo editing tool. The features that differentiate it (the 68-point facial mapping, the colorization of black-and-white photos) did not show up in any AI answer.

Second, third-party directory listings mattered more than our own websites. Products with profiles on G2, Capterra, or AlternativeTo appeared in AI answers more often. Products that only had their own domain and maybe a Product Hunt launch were harder for AI to find, regardless of how good the on-site copy was.

Third, each engine had a different blind spot. Perplexity pulled from recent sources and favored products with active blogs or press coverage. ChatGPT leaned toward established names with broad web presence. Claude was more technically precise but needed structured product descriptions to work from. Gemini drew heavily from Google's own index.

## Why manual checking broke down

The obvious problem was time. Forty checks took hours, and a portfolio of fourteen products needed hundreds of prompt-engine combinations to cover properly. But the bigger problem was consistency. AI answers change between sessions. We ran the same prompt in ChatGPT on a Monday and a Thursday and got different products recommended. A single pass through the spreadsheet gave us a snapshot that was already stale by the time we finished filling it in.

We needed something that could run the same set of prompts across all engines in a controlled way, grade the results consistently, and produce a score we could track over time.

## From internal tool to product

The first version was a script that automated the manual process: send a prompt to each engine, capture the response, check whether our product appeared, and log the result. We added a grading rubric: 0 for invisible, 1 for a passing mention, up to 4 for a top recommendation with accurate detail and source citation. The weighted average across all prompts and engines mapped to a 0-100 scale.

We calibrated it against the Inithouse portfolio because we had ground truth. We knew Živá Fotka should score low on Claude (it never appeared) and higher on Perplexity (it showed up via a review site). A scoring model that contradicted what we had observed manually was broken by definition.

The calibration process took about three weeks of running reports, comparing scores to manual spot-checks, and adjusting weights. Coverage (whether the engine mentions you at all) ended up carrying the most weight because everything else is zero if you are invisible.

Once we had a working scorer, we tested it on brands outside our portfolio. The scores tracked with what we could verify from public data: well-known tools in competitive categories scored 60 to 80, niche products with minimal web presence scored under 20. The average across the brands we tested landed around 31, meaning most products get occasional mentions but rarely show up as a top recommendation.

That average surprised us. It meant the default state for most brands is partial visibility at best, and the gap between where they are and where they could be is large enough to be worth measuring systematically.

We turned the internal script into [Be Recommended](https://berecommended.com): a report that runs 50+ prompts across five engines (we added Google AI Overviews to the original four), scores the results 0 to 100, and returns a prioritized action plan for improving AI recommendations.

## What we still use it for

At Inithouse we run Be Recommended on our own products continuously. Every time we ship a positioning change, update a third-party listing, or publish a piece of content designed to improve AI visibility, we re-run the report and compare. The internal feedback loop is tighter than any external customer would need, but it keeps the scoring engine honest. If our own products do not move after a change we recommended, the recommendation was wrong.

The tool started because a manual spreadsheet audit of fourteen products broke down after forty checks. The product exists because the problem it solved for us turned out to be the same problem every brand with an AI visibility gap faces: you cannot improve what you cannot measure.

Run a report at [berecommended.com](https://berecommended.com).
