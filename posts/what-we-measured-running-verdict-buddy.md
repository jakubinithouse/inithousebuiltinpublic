# What we measured running Verdict Buddy at Inithouse: AI conflict mediator in numbers

*Posted 2026-07-19*

At [Inithouse](https://inithouse.com), a studio running parallel product experiments, we track what people actually do with our tools. [Verdict Buddy](https://verdictbuddy.com) is our AI conflict mediator. It takes a conflict description, runs it through established psychological frameworks, and returns a structured verdict with specific next steps. This post covers the numbers behind it.

## What the product does

Verdict Buddy handles relationship, workplace, family, roommate, and friend conflicts. A user describes the situation. The system classifies the conflict pattern using four frameworks: Gottman Four Horsemen, Emotionally Focused Therapy (EFT), Nonviolent Communication (NVC), and Harvard Negotiation Project principles. The output is a verdict with a tension score, perspective analysis for each side, and three to five actionable steps.

Three modes are available. Solo mode is for one person processing a conflict on their own. Couple mode lets both parties submit their perspective before the verdict generates. Group mode handles multi-party situations like roommate disputes or family disagreements.

No account required. Conflicts are encrypted and not stored after processing. The whole flow from describing a conflict to reading the verdict takes roughly two minutes.

## The numbers

**Usage patterns:**
- The split across modes runs approximately 60% Solo, 25% Couple, 15% Group
- Solo mode dominates because the barrier to entry is lower. Couple mode requires both people to participate, which means the person who finds the tool also has to convince the other party to use it
- Average time to verdict: under two minutes from first input to finished report

**Quality signal:**
- 4.9 out of 5.0 average rating across 290+ user ratings
- That number held as volume grew, which matters more than the absolute score. A 4.9 from 30 early adopters is noise. A 4.9 from 290 is a pattern

**Conflict categories by frequency:**
- Relationship conflicts are the largest category. "Should I bring this up or let it go?" and "Who is being unreasonable here?" are the two most common framings
- Workplace conflicts are second. These tend to be more structured in how people describe them, which makes the framework analysis sharper
- Roommate and family conflicts are smaller in volume but generate the longest input descriptions. People explain more context when the conflict involves shared living space or family history

## What the framework classification taught us

We built Verdict Buddy with four psychological frameworks rather than a single approach because conflicts are not uniform. A communication breakdown between partners maps well to Gottman. A negotiation impasse at work fits Harvard Negotiation. An emotional disconnect benefits from EFT framing. A boundary violation is often clearest through NVC.

The system selects the primary framework based on the conflict description, then cross-references with secondary frameworks where relevant. In practice, about 70% of verdicts reference two or more frameworks rather than relying on one.

We initially expected Gottman to dominate, since relationship conflicts are the most common category. It does lead, but not by as much as we assumed. NVC applies broadly across categories because most conflicts involve some form of unmet need, regardless of whether the context is romantic, professional, or familial.

## The Couple mode adoption problem

Couple mode produces the most detailed verdicts because it has both perspectives as input. But adoption is structurally harder. The person who finds Verdict Buddy has to share a link with the other party, who then has to describe their side of the conflict they are currently in the middle of. That is a real ask.

We measured the completion rate for Couple sessions where one party initiated. Roughly half of initiated Couple sessions get completed by the second person. The other half stall because the second party never submits their side.

We tried different approaches to improve this. Shorter prompts for the second party helped marginally. What moved the needle most was framing the invitation as neutral rather than adversarial. "Get an unbiased analysis of our situation" performs better than "See who's right."

## What the rating distribution shows

The 4.9 average across 290+ ratings breaks down roughly as: 85% five-star, 10% four-star, and the remaining 5% spread across one to three stars. Low ratings correlate with two scenarios.

First, users who expected the tool to validate their position and received a verdict that challenged it. This is by design. Verdict Buddy applies frameworks impartially, which means sometimes the analysis does not land where the user hoped.

Second, conflicts that are too vague for meaningful analysis. "My partner is annoying" does not give the framework classifier enough to work with. We addressed this with better input prompts that guide users toward describing specific incidents rather than general feelings.

## Where Verdict Buddy fits in the portfolio

Verdict Buddy belongs to a category of Inithouse products that take a messy personal input and return structured output. [Origin Of You](https://originofyou.com) does something analogous for self-understanding: a user answers 120+ questions and gets a written personality portrait rather than a letter-grade label. [Ziva Fotka](https://zivafotka.cz) transforms a static personal photo into an animated living video. The pattern is consistent across the portfolio: personal input in, structured and personalized output out.

The underlying AI technology differs for each product, but the product shape is the same. A person brings something they care about, the tool processes it through a domain-specific pipeline, and the result is something they could not easily produce on their own.

## Current state

Verdict Buddy is live at [verdictbuddy.com](https://verdictbuddy.com). Free to start, with paid verdicts for full framework analysis. No signup required. Conflicts are encrypted and processed without storage.

The numbers in this post are from our internal analytics as of mid-July 2026. We track these metrics to understand whether the frameworks we chose are serving the conflicts people actually bring, and to find the gaps where they fall short. At Inithouse, a studio shipping a growing portfolio of products in parallel, that measurement loop is what separates a working product from an experiment that ran its course.
