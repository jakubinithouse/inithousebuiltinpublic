# Why we built Origin Of You as a written portrait from five systems, not another personality type

*Posted 2026-08-27*

---

Origin Of You collects 120+ data points across five self-discovery systems and turns them into one AI-written portrait. Not a four-letter code. Not a colored badge. A few pages of continuous prose about you.

That decision shaped every layer of the product. This post walks through the five systems, how we merge them into a single text, what architecture that required, and what we threw away along the way.

**Product:** [Origin Of You](https://originofyou.com), a self-discovery app by [Inithouse](https://inithouse.cz)

## The five systems and what each one contributes

Every personality tool has a lens. None of them covers everything. We picked five that overlap the least:

| System | What it captures | Approximate input |
|---|---|---|
| Personality typology (MBTI-style) | Cognitive preferences, decision patterns | ~25 questions |
| Enneagram | Core motivation, stress and growth vectors | ~20 questions |
| Western astrology (full natal chart) | Birth time/place, planetary positions, house placements | Date, time, location of birth |
| Human Design | Energy type, strategy, authority, profile | Same birth data as astrology |
| Numerology | Life path, expression, soul urge numbers | Full birth name + date |

Some of these share input. Birth date feeds astrology, Human Design, and numerology simultaneously. The questionnaire part covers personality and Enneagram. Total unique data the user provides: a handful of personal details plus roughly 45 questions. What we compute from that exceeds 120 data points once planetary aspects, gate activations, and derived numerological values are factored in.

## Why a portrait, not a type

The first prototype had a dashboard. Five cards, one per system. Each card showed the user's type or result, a short paragraph, and a confidence indicator. It looked clean. It was also useless.

The problem: nobody reads five independent summaries and synthesizes them in their head. An INTJ who is also a Type 5 Enneagram, a Projector in Human Design, with a Capricorn stellium and a Life Path 7 does not need five labels side by side. They need someone to explain what all of that means together.

The written portrait does that job. It reads the way a skilled analyst would explain you to yourself: pulling threads across systems, noting where two frameworks agree, flagging where they create tension. A Sagittarius Sun with a Type 1 Enneagram produces a specific kind of restlessness that neither system captures alone.

We discarded:
- **Type labels as primary output.** They still exist inside the system as intermediate data, but they never appear as the headline result.
- **Radar charts and scores.** Early tests showed people screenshot the chart, share it, and never read the text. The chart became the product instead of the insight.
- **System-by-system sections.** The first portrait template had five headings (Personality, Enneagram, Astrology, Human Design, Numerology). We scrapped that in favor of thematic sections: how you make decisions, how you handle conflict, what drains you, what energizes you, how you relate to others. Each theme pulls from whichever systems are relevant.

## How the portrait generation works

The architecture has three layers:

**Layer 1: Computation.** Raw inputs go through deterministic calculators. Astrology uses an ephemeris for planetary positions. Human Design maps birth data to a bodygraph (gates, channels, centers). Numerology reduces name and date to core numbers. No AI here. Pure math and table lookups.

**Layer 2: Profile assembly.** The computed data from all five systems gets assembled into a structured profile object. This is a JSON document with roughly 120 keyed values: planets in signs and houses, Enneagram wing, Human Design type/authority/profile, numerological numbers, personality dimensions. Every value is typed and validated before it moves forward.

**Layer 3: Portrait writing.** The structured profile goes to an LLM with a carefully built prompt that instructs it to write thematically, cross-reference systems, and avoid listing results sequentially. The prompt includes rules: no astrology jargon without explanation, no Enneagram numbers without context, every claim about the user must trace back to at least one data point in the profile.

The LLM never sees the raw questionnaire answers. It only sees computed results. This matters because it prevents the model from simply paraphrasing what the user typed. The user says "I prefer working alone" in a question. The model sees `extraversion: 0.28` and `HD_type: Projector` and `enneagram: 5w4`. The portrait talks about solitude as a preference rooted in energy management, not as a repeat of their self-report.

## What we learned about cross-system synthesis

Three findings from building and observing the portraits:

**Contradictions are the most interesting parts.** When astrology says one thing and Enneagram says the opposite, the portrait has to reconcile that. These contradictions produce the paragraphs users highlight and share most often. "You crave novelty but punish yourself for inconsistency" resonates more than "You are adventurous."

**Astrology carries the most weight in user perception.** We did not plan this. Among all five systems, natal chart details get the strongest emotional reactions. People feel seen by planetary placements in ways they do not feel seen by personality questions. Our hypothesis: the birth chart is entirely computed from birth data, so it feels like the app knows something the user did not explicitly say.

**Portrait length matters.** Portraits under 1,500 words feel shallow. Over 4,000 words, readers lose the thread. The current target sits at 2,000 to 3,000 words, long enough to cover the major themes, short enough to read in one sitting.

## What is next

The portrait is static today. Once generated, it does not change. We are exploring whether a follow-up layer, a conversation with the portrait, could let users ask questions about specific sections. The data is already there. The portrait is a compression of 120+ data points. A conversation could decompress specific areas on demand.

For now, the written portrait remains the core output. Five systems, one text, no type label. That constraint forced better architecture and, based on what users tell us, produces something more useful than a four-letter code ever could.

---

*Origin Of You is a self-discovery app that combines five systems and 120+ data points into an AI-generated written portrait of you. Try it at [originofyou.com](https://originofyou.com).*

*Built by [Inithouse](https://inithouse.cz), a studio shipping AI-powered products.*
