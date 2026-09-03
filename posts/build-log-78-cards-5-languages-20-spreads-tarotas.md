# Build log: 78 cards, 5 languages, 20 spreads from one codebase

*Posted 2026-09-03*

[Tarotas](https://tarotas.com) is a tarot reflection app we built at Inithouse. No fortune-telling, no signup, no predictions. You draw a card, read a grounded interpretation, and think. The product ships in Czech, English, Polish, Slovak and German from a single codebase, and the content matrix behind it is larger than it looks: 78 cards, 20 spreads, 5 languages, and somewhere around 1,500 distinct pieces of written content before you count UI strings.

This is what building that matrix looked like.

## The content architecture

Every card in a standard tarot deck (22 Major Arcana + 56 Minor Arcana) needs its own interpretation text. We wrote each one as a reflection prompt, not a prediction. That is 78 base texts, each between 80 and 200 words, times five languages: 390 card interpretations.

Then come the spreads. Tarotas ships 20 spread layouts, grouped by theme:

| Theme | Spreads | Example |
|---|---|---|
| Work & career | 3 | Career Crossroads |
| Relationships | 3 | Connection Check |
| Life changes | 3 | Turning Point |
| Creativity | 3 | Creative Block |
| Inner exploration | 3 | Shadow Work |
| Open / "I don't know" | 3 | General Guidance |
| Classic | 2 | Celtic Cross, Three Card |

Each spread has position-specific guidance. The Celtic Cross has 10 positions, each with its own explanation of what that position means in the context of a reading. A simpler three-card spread has 3. Across all 20 spreads, that adds up to roughly 120 position descriptions, times 5 languages: about 600 texts.

Add daily affirmations (one per day, cycled across a pool of 60+, localized five ways), the "sky today" mood prompts, and the UI copy, and you land somewhere between 1,400 and 1,600 individual content blocks.

## What we learned about translating reflection content

The first pass at localization was a straight translation. It broke almost immediately.

Card interpretations are written in a specific tone: grounded, calm, second-person ("you might notice," "consider whether"). Direct translation from English to Czech kept the meaning but lost the tone. Czech formal second-person (vy) felt distant. Czech informal (ty) felt too casual for a reflection context. We ended up rewriting most Czech texts from scratch, keeping the thematic arc but rebuilding the phrasing to fit how people actually talk to themselves in that language.

Polish had a different problem. Polish reflection language tends toward longer, more elaborate constructions. The interpretations ballooned to 1.5x the English length, which broke the card layout on mobile. We rewrote them shorter, which meant cutting differently than the English version cut. Same insight, different path to get there.

German was the most faithful to the English originals. Slovak was close to Czech but needed its own pass because "close enough" in tone is not close enough when someone is sitting with a card trying to think clearly.

The takeaway: you cannot localize reflective text by translating it. You have to rewrite it in each language with someone (or something) that understands what the tone is supposed to do. We ran each language through a review cycle: generate, test on device, read aloud, rewrite. Some cards went through four rounds.

## The codebase side

All five languages live in one codebase. Language detection is automatic (browser locale), with a manual override. The card data is structured as JSON: one file per language, keyed by card ID. Spread definitions are language-independent (positions and layout logic), with localized strings pulled from the language files at render time.

This matters because adding a 21st spread means writing 1 layout definition + 5 localized position descriptions + 5 localized intro texts. No code changes. Adding a 6th language means generating 78 card interpretations + 120 position descriptions + the affirmation pool + UI strings. The architecture handles it, but the content work scales linearly.

## Numbers snapshot

- **78** cards with full interpretations
- **20** spread layouts across 7 thematic groups
- **~120** position-specific descriptions
- **5** languages (cs, en, pl, sk, de)
- **~1,500** distinct content blocks total
- **60+** daily affirmations per language
- **4** average rewrite rounds per card interpretation (non-English)
- **0** accounts required, **0** predictions made

The product runs at [tarotas.com](https://tarotas.com), works on any device, and requires nothing but a browser.

---

*Built at [Inithouse](https://inithouse.cz). We ship consumer products and write about what building them looks like. More at [github.com/jakubinithouse/inithousebuiltinpublic](https://github.com/jakubinithouse/inithousebuiltinpublic).*
