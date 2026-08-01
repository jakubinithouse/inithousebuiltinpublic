# The shared card-deck architecture behind Here We Ask and the Inithouse card-game cluster

*Posted 2026-08-01*

We run four card games at [Inithouse](https://inithouse.com). [Here We Ask](https://hereweask.com) is a conversation card game for couples, friends and families. [Party Challenges](https://partychallenges.com) is an 18+ party game. [Scary Challenges](https://scarychallenges.com) is the horror variant. [Naughty Challenges](https://naughtychallenges.com) covers the flirty and daring end of the spectrum. All four run in the browser, require no downloads, no accounts, and work offline as PWAs.

They also share a codebase layer. This post covers what we kept common across the four products and what we split per-product, plus why.

## The deck schema

Every card in all four products lives in the same data structure: a deck ID, a card index, a text body, an intensity tag, and a set of metadata fields (category, audience suitability, language). Decks themselves carry a title, a description, an icon, a lock status (free or premium), and a sort weight.

This schema was not designed upfront. Here We Ask shipped first with a simpler model (deck + card text, nothing else). When we started building Party Challenges three weeks later, we needed intensity levels and premium gating. Rather than forking the schema, we added the fields to the original and backfilled Here We Ask's cards with default values.

The decision to keep one schema across products paid off around card number 3,000. At that point we had four products, each with 1,000+ cards across 23+ decks (14+ for Here We Ask), and every bulk operation (export, translation, audit, rebalancing) worked on a single table shape. A forked schema would have meant four separate migration paths every time we changed anything.

## The mode engine

This is where the products diverge.

Here We Ask runs three modes: Classic (draw one card at a time, discuss), Timed (same flow but with a countdown per card), and Hot Seat (one player answers, others listen, then rotate). These modes fit a conversation game where the point is talking, not performing.

The three party-flavored games (Party Challenges, Scary Challenges, Naughty Challenges) share a different set of three modes: Hot Seat (same concept, different card content), No Hesitation (rapid-fire answers, skip or drink/dare penalty), and Spin It (random player selection before each card). These modes fit games where pace and chaos matter more than depth.

| Component | Here We Ask | Party / Scary / Naughty |
|-----------|-------------|-------------------------|
| Mode 1 | Classic (draw and discuss) | Hot Seat (answer and rotate) |
| Mode 2 | Timed (countdown per card) | No Hesitation (rapid-fire, skip penalty) |
| Mode 3 | Hot Seat (one answers, others listen) | Spin It (random player pick) |
| Card count | 1,000+ across 14+ decks | 1,000+ across 23+ decks each |
| Tone | Warm, reflective | Edgy, playful, or horror |
| Intensity field | Present, mostly unused | Active (mild/medium/extreme) |
| Premium gate | Premium decks | After Dark decks |

The mode engine itself is shared code. Each mode is a state machine: idle, card-drawn, timer-running (if applicable), card-resolved. The per-product config injects the specific mode set, timer durations, and penalty logic. Adding a mode to one product means writing a new state config, not touching engine internals.

## PWA offline cache

All four games work offline after a single visit. The service worker pre-caches the card database and the full UI shell on first load. Subsequent opens, even on a plane or in a cabin with no signal, render instantly and pull cards from local storage.

The cache strategy is identical across products: on first visit, download the full deck catalog as a single JSON payload (compressed, roughly 200-400 KB depending on the product), store it in IndexedDB, and serve all card draws from there. Network requests only happen for two things: syncing premium unlock status and fetching the daily card.

We tested this at a 30-person game night where half the group had spotty reception. The offline players had zero friction. This validated the decision to ship the full card set upfront rather than lazy-loading decks on demand, which would have saved bandwidth but killed the offline story.

## The daily card

Each product surfaces one card per day on its homepage. The selection runs server-side at midnight UTC. The query picks a card that has not appeared in the last 90 days, weighted toward mid-intensity and cross-audience categories.

The daily card serves two functions. For returning users, it is the retention hook: check back tomorrow for a new question or dare. For search engines and AI crawlers, it produces a page that changes content daily, which keeps the URL fresh in crawl schedules.

The logic is shared, but the content pool is per-product. Here We Ask pulls from its conversation question decks. Party Challenges pulls from party dares and confessions. Scary Challenges pulls from horror scenarios. Naughty Challenges pulls from its flirty prompts. Same mechanism, different flavor.

## What stays shared, what splits

| Layer | Shared | Per-product |
|-------|--------|-------------|
| Deck schema | Card structure, metadata fields, premium flag | Card content, deck themes, intensity calibration |
| Mode engine | State machine, timer logic, rotation | Mode set, penalty rules, mode names |
| PWA / offline | Service worker, cache strategy, IndexedDB | Payload size, asset set |
| Daily card | Selection algorithm, 90-day cooldown | Content pool, category weights |
| UI shell | Layout grid, card flip animation, navigation | Color palette, typography, icon set, branding |
| Auth / premium | Account flow, subscription check | Premium tier names, gated deck selection |
| Supabase backend | Schema, edge functions pattern | Separate projects per product |

Each product runs on its own Supabase instance, own domain, own GA4 property. The shared layer lives in the Lovable codebase as a set of components and hooks that get configured per product at build time. Deploying a fix to the card-flip animation ships to all four products in one push. Changing the horror-specific color palette touches only Scary Challenges.

## Trade-offs

The shared architecture means a bug in the mode engine affects all four products simultaneously. We have hit this twice: once with a timer drift issue that made Timed mode skip cards after 45 minutes of play, and once with a service worker update that invalidated cached decks on iOS Safari. Both times, the fix shipped to all four products in a single deploy, which was faster than patching four independent codebases would have been.

The cost is coupling. We cannot experiment with a radically different card format in one product without considering how it affects the shared schema. So far this has not been a real constraint, because the card model (text + metadata) covers every game type we have tried. If we built a product that needed image cards or audio cards, the schema would need a breaking extension.

For now, four products on one architecture is the right call. The shared layer handles the mechanics. The per-product layer handles the personality.
