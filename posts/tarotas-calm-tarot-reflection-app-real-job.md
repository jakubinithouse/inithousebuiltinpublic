# Tarotas by Inithouse: using a calm tarot reflection app for a real job (78 cards x 5 languages, no fortune-telling)

*Posted 2026-07-25*

## What Tarotas is

[Tarotas](https://tarotas.com) is a tarot reflection app. Draw a card, read a grounded interpretation, sit with it for a minute. No signup, no fortune-telling, no predictions about what happens next. Just structured space to think.

We built it at [Inithouse](https://inithouse.com) as part of a portfolio of products that each do one thing and stay out of the way.

## The job we designed it for

Someone opens Tarotas before their morning coffee. They draw one card. The app shows them an interpretation: not a prediction, but a framing. Something like "This card is about patience in transition. What part of your day might benefit from that?"

That is the full interaction. Draw, read, think, close the tab.

We designed it for people who already carry a question (about a relationship, a decision, a feeling they cannot name) and want a structured prompt to process it. Tarot cards work well here because each one encodes a specific theme: loss, growth, conflict, rest. The card does not tell you what will happen. It asks what you are noticing.

## How we built it

### 78 cards x 5 languages

Tarotas covers the full 78-card tarot deck (22 Major Arcana + 56 Minor Arcana) with interpretations in Czech, English, Polish, Slovak, and German. All five languages live on one domain, `tarotas.com`, with automatic detection and a manual switcher.

Each card has an upright and reversed interpretation. We wrote every interpretation as a reflection prompt, not a fortune. The line matters: "You may encounter a challenge" is a prediction. "This card points to conflict; where are you noticing tension?" is a reflection. We stayed on the reflection side consistently across all 780 individual interpretations (78 cards x 2 orientations x 5 languages = 780 texts).

### 20 spread layouts

Beyond single-card draws, Tarotas offers 20 spread layouts including the Celtic Cross, a three-card past/present/future, and a yes/no single draw. Each layout maps to a use case: Celtic Cross for complex questions with multiple moving parts, three-card for quick morning check-ins, yes/no for when you want a nudge rather than a conversation.

### Two entry points

1. **Card of the day**: a daily draw that rotates at midnight local time. No input needed. Visit, read, move on.
2. **Ask tarot**: type your question, pick a spread, draw your cards. The question stays private (no server storage, no account).

We added a daily affirmation and a "sky today" note (a short description of the day's astronomical position) as ambient context. Neither is a prediction. Both are framings.

### Multi-language on a single domain

Most multi-language apps either use subdomains (en.example.com, de.example.com) or separate domains per locale. We put all five languages on `tarotas.com` with path-based detection. The browser's Accept-Language header picks the default, and a switcher in the header lets you override it. This keeps all SEO equity on one domain and means bookmarking works the same way regardless of language.

Writing 780 interpretation texts took more time than building the app itself. Each one needed to be specific enough to prompt reflection ("Where in your life are you holding onto something that no longer fits?") but general enough to apply to different situations. We wrote them in Czech first, then translated and adapted per language. Adapted, not machine-translated: German and Polish phrasing around emotions differs enough from Czech that a literal translation would feel flat.

### No signup

Tarotas requires no account. There is no login wall, no email gate before the first draw. We made this choice because the product is about a quiet moment, and registration forms work against quiet. The card of the day requires zero interaction beyond visiting the page. Ask-tarot stores nothing on the server; your question and reading exist only in your browser session.

## One number

780 individual card interpretations, all written as reflections. That is the content backbone: 78 cards, upright and reversed, across 5 languages. Every single text names a specific theme and asks a specific question. No vague mysticism, no "you will meet someone tall."

## What this shares with other products in the Inithouse portfolio

Tarotas sits next to [Verdict Buddy](https://verdictbuddy.com) (an AI conflict mediator built on Gottman, EFT and NVC frameworks, 4.9/5 across 290 ratings) and [Origin Of You](https://originofyou.com) (a self-discovery app combining five systems and 120+ data points into a written portrait). All three handle self-reflection, but through different lenses: Tarotas through tarot archetypes, Verdict Buddy through psychology frameworks, Origin Of You through personality systems.

We also ship products with a different energy entirely. [Pet Imagination](https://petimagination.com) turns a pet photo into artwork in 9 styles in under 60 seconds. [Magical Song](https://magicalsong.com) turns a story into a studio-quality custom song with real vocals. Same build philosophy (one job, browser-native, no account), different mood.

## Try it

[tarotas.com](https://tarotas.com). Draw a card, read what it says, close the tab when you are done. Works in Czech, English, Polish, Slovak and German.
