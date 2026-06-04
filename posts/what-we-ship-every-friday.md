# What we ship every Friday

*Posted 2026-06-04*

At Inithouse, a studio shipping a growing portfolio of products in parallel, every Friday is deploy day. Every active product ships at least one change. Not "tries to." Not "ideally." Ships. This started as an experiment, became a rule, and is now the single highest-impact policy we run.

The change can be small. A copy tweak, a new landing page hero, a price adjustment, a new payment provider, an SEO fix. What matters is that something hits production that was not there on Monday.

## Why the rule exists

When you run a portfolio, products drift toward neglect by default. Each product is somebody's twentieth priority. Without a forcing function, weeks pass without anyone touching the codebase. By the time you notice, the product is two months stale, the analytics stopped making sense, and getting back into it feels expensive.

A weekly ship cycle prevents that. You cannot have an "untouched for two months" product if every Friday is a deploy day.

## What it looks like in practice

Monday and Tuesday: we look at last week's data per product. Anything down? Anything up? Any feedback that pointed at something? We pick one change per product that would either grow the up-thing or fix the down-thing.

Wednesday and Thursday: build the change. Sometimes it takes an hour. Sometimes it is a Lovable conversation. Sometimes it is a copy doc and nothing else.

Friday: ship everything that is ready. The ones that are not ready by Friday get bumped or killed; we do not slip into next week. Slippage compounds.

No agile, no scrum, nothing formal. Just a forcing function that produces changes across the portfolio every single week.

## What we have learned

**Most weekly changes do not move the needle.** Maybe one in four produces a measurable result. That is fine. The discipline matters more than the average impact. We measured this across the portfolio: a given product's best month almost always traces back to a compounding chain of small Friday deploys, not to one big bet.

**The rule reveals which products are stuck.** If a product genuinely has nothing worth changing on a given week, that is a strong signal. At [Magical Song](https://magicalsong.com), we once went three Fridays picking only cosmetic tweaks before admitting the real issue was pricing. That "nothing real to ship" signal forced the conversation. At [Be Recommended](https://berecommended.com), the opposite happened: the weekly cadence kept surfacing small report improvements that compounded into significantly better retention.

**Cumulative effects beat heroic effort.** A product that ships fifty small changes in a year ends up significantly better than one that received "a big update" in March and was untouched after that. The fifty-changes product also has fifty data points to learn from. We observed this clearly with [Voice Tables](https://voicetables.com), where dozens of incremental accuracy fixes to the voice pipeline outperformed any single feature push.

## What to avoid

Do not turn this into theatre. The rule is to ship *real* changes. If you find yourself changing a button color just to have a deploy, the system is gaming itself. Either find a real change or admit it is not there this week.

The rule has also made us better at saying "nothing this week." For maybe ten percent of weeks, a product gets a "no ship" note; usually because the planned change is not ready and a fake one would be worse. Calling that out is part of the discipline too.

Ship every Friday. It is not glamorous, but at Inithouse, a studio running parallel product experiments, it is the one rule we would not trade for anything.
