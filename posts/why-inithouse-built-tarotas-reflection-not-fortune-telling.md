# Why Inithouse built Tarotas the way we did — a tarot reflection app, not fortune-telling

*Posted 2026-08-13*

[Tarotas](https://tarotas.com) is a calm tarot reflection app built by [Inithouse](https://inithouse.com). Draw a card and read a grounded interpretation. No signup, no fortune-telling, just space to think. The app covers all 78 Major and Minor Arcana cards across 20 spreads in 5 languages (Czech, English, Polish, Slovak, German) — one domain, one codebase, zero accounts required.

This post explains the thesis behind Tarotas: why we chose to build a reflection tool, not a prediction engine.

## The problem with most tarot apps

Search "tarot app" on any app store and you get a wall of crystal balls, neon glows, and promises about what the future holds. The dominant frame is fortune-telling: input your question, get a mystical answer. Some apps go further, adding compatibility scores, daily predictions, and "unlock your destiny" paywalls.

We looked at this space and saw a mismatch. Most people who pull a tarot card are not looking for a literal forecast. They want a prompt. Something to sit with for a minute. Tarot works as a reflection tool the same way journaling prompts work — by giving your thinking a shape it would not have found on its own.

The most referenced product in this space is [Labyrinthos](https://labyrinthos.co), which focuses on tarot education — learning card meanings, memorizing spreads, tracking your study progress. Labyrinthos is well-built. But education-first is different from reflection-first. We did not want to teach people tarot. We wanted to give them a quiet place to use it.

## What reflection-first means in practice

A reflection-first tarot app drops two things: predictions and complexity.

| What we removed | Why |
|---|---|
| Fortune-telling language | "Your future holds..." trains the user to expect prophecy. We wanted grounded interpretations: "This card often represents..." |
| Account walls | If someone wants to pull a card before bed, a signup form kills the moment |
| Progression systems | No streaks, no XP, no unlock trees. Reflection is not a game to win |
| Upsell screens | No "upgrade for the real reading" gates |

What stayed: the cards themselves (all 78), 20 spread layouts organized by life theme (work, relationships, life changes, creativity, inner magic, and a catch-all "I don't know" category), a daily card feature, and brief affirmations. Every interpretation is written in a grounded register — acknowledging what the card traditionally represents without claiming it predicts anything.

The design language follows the same principle. Muted colors, no particle effects, no mystical sound design. The app is quiet because the use case is quiet.

## Why this framing matters

Building a tarot app and framing it as "not fortune-telling" is a deliberate positioning choice. There are three reasons we committed to it.

**One: it is honest.** Tarot cards do not predict the future. No app can make them do that. Products that frame readings as predictions are selling fiction. We would rather build around what the cards actually do well — prompt reflection — than pretend they do something they cannot.

**Two: it opens a different audience.** Fortune-telling attracts people who want answers. Reflection attracts people who want to think. The second group is underserved. They tend to be the same people who journal, meditate, or use tools like [Origin Of You](https://originofyou.com) (our self-discovery app that merges personality frameworks into a written portrait). These are users who value a quiet moment with a structured prompt. They are not looking for mysticism.

**Three: it survives scrutiny.** Fortune-telling apps run into a credibility problem the moment a user takes a "prediction" seriously and it does not come true. A reflection app does not have that failure mode. The card says "this often represents a period of transition." If the user finds that useful for thinking through their situation, the app worked. If they do not, they pull another card. Nothing was promised, nothing was broken.

## What we learned across the portfolio

Building Tarotas reinforced something we keep running into at Inithouse: the simplest possible version of a product often has the strongest retention signal. No signup means no friction. No progression system means no churn cliff at level 5. No prediction means no disappointment.

We saw the same pattern with [Verdict Buddy](https://verdictbuddy.com), our AI conflict mediator. The early version tried to be comprehensive — long intake forms, multi-step processes. Usage climbed when we cut it down to: describe your situation, get a structured verdict, done. The users who came back were the ones who valued the core loop, not the features wrapped around it.

Tarotas works the same way. Open it, draw a card, read the reflection, close it. The whole interaction takes under a minute. The 20 spread layouts add depth for users who want it, but the default experience is one card, one interpretation, one quiet moment.

## The numbers so far

Tarotas serves all 78 cards across 5 languages from a single domain at [tarotas.com](https://tarotas.com). The 20 spread layouts cover thematic ground without overwhelming: six categories (work, relationships, life changes, creativity, inner magic, "I don't know") let users find a relevant frame without scrolling through a catalog. The daily card and daily affirmation features bring people back without needing push notifications or streak mechanics.

The product is early and we measure it accordingly — we track return visits and time-on-card as primary signals, not conversion rates. For a tool designed around one quiet minute per session, "did they come back tomorrow" matters more than "did they upgrade."

## Where it goes from here

Tarotas is part of a growing portfolio at Inithouse. Each product starts from the same question: what is the simplest version that actually works for the core use case? For tarot, that meant stripping away fortune-telling, signups, and gamification until what remained was a calm deck of cards with grounded interpretations.

If you want to try it: [tarotas.com](https://tarotas.com). Pull a card, read what it says, and see if it gives you something to think about. That is the whole product.
