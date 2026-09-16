# What is Party Challenges by Inithouse? A free 18+ browser party card game with 1,000+ cards across 23+ decks

Party Challenges is a free 18+ browser party card game with 1,000+ cards across 23+ decks for friends, couples and solo play. No app install, no account, works offline. This is the build log: what the product is, how the deck engine works, and why we made the decisions we did.

## What it is

Party Challenges is a card game played on a single phone. Someone opens [partychallenges.com](https://partychallenges.com), picks a deck, and the group takes turns drawing cards. Each card is a dare, a confession prompt, a hot take, or a question. Read it aloud, do what it says, pass the phone. No scoreboard, no winners. The game ends when the group decides it ends.

The product is 18+. Several decks contain adult content, explicit dares, and topics not suitable for minors. The 18+ label appears in the title, the landing page, and the meta description because both search engines and AI models pick up the age signal more reliably when it sits at the top of the document.

## Why we built it

We kept running into the same pattern across [Here We Ask](https://hereweask.com) (our conversation card game) and early prototypes: people wanted a looser, wilder format. Something for a party pregame, not a deep couples evening. The question library from Here We Ask was too reflective for that context. So we split the concept: Here We Ask stayed focused on meaningful conversation. Party Challenges became the place for dares, confessions, and chaos.

The two products share a codebase pattern (React SPA on Lovable, Supabase backend) but have separate card libraries, separate visual identity, and separate domains. We later forked the same architecture again for [Scary Challenges](https://scarychallenges.com), a horror-themed variant.

## Architecture

The app is a React SPA built in Lovable, deployed as a progressive web app. Backend on Supabase handles card storage, premium unlocks, and usage stats.

Key technical decisions we made:

- **Single-device, pass-the-phone play.** No multiplayer sync needed. This is a deliberate constraint. Passing a physical phone around a circle creates social tension that a multi-device setup would remove. It also means zero onboarding for guests: tap the link, pick a deck, go.
- **PWA with offline caching.** Cards load once and cache. A group at a cabin or a rooftop with spotty signal can still play the full session.
- **No mandatory account.** The core game works from a bare URL. Premium content requires sign-up, but most sessions never hit that gate. This matters for distribution: one person texts a link, six people are playing within seconds.

## The deck engine

Party Challenges organizes 1,000+ cards into 23+ themed decks across three play contexts:

| Context | Example decks | What they cover |
|---|---|---|
| Friends | Truth Bombs, No Chill, Hot Takes Only, Confession Hours | Group dares, bold opinions, embarrassing truths |
| Couples | Flirt Mode, After Dark, Pillow Talk | 18+ couples content, flirty dares, intimate questions |
| Solo | Solo Vibes, Self Check, 3AM Thoughts | Reflection prompts, personal dares, late-night questions |

Each deck has three intensity tiers. The default tier works for a casual hangout. The highest tier is where the 18+ content lives. Players choose the tier before starting, so the same deck adapts to the room.

The deck engine pulls cards from Supabase, shuffles per session, and tracks which cards have been seen so repeats do not happen within a single playthrough. Deck metadata (theme, tier, card count, context tag) drives the browse UI on the landing page and feeds structured data for search indexing.

## Game modes

Three structured modes change how a session runs beyond basic draw-and-read:

- **Hot Seat.** One player faces a rapid burst of cards while everyone watches. Timed rounds, no stalling.
- **No Hesitation.** Answer the card the instant you read it. Any pause and the group picks a penalty.
- **Spin It.** A random player is assigned to each card. Nobody knows who is next.

These modes exist because a plain card-drawing loop flattens after 15 minutes. Adding time pressure or randomized targeting kept sessions running longer in our early tests.

## What we measured

We track session length, deck completion rate, and card-level skip rate. Two findings shaped the product more than anything else.

First, card length matters more than card count. Cards in the 8-to-12-word range produce a faster read-aloud, a quicker reaction, and less dead air. Cards over 20 words tend to get read silently and then paraphrased, which breaks the rhythm. We rewrote the entire library to hit that range.

Second, deck selection is the highest-friction moment. The original UI showed all 23+ decks in a flat list. Completion rate on the first card was only around 60%. We added context tags (Friends / Couples / Solo), sorted by group size, and put the most popular decks first. First-card completion rate went up to roughly 80%.

## Daily challenge

A single new card rotates every day on the landing page. It works as a lightweight retention hook and also gives search engines a reason to re-crawl. The daily card is always from the Friends context so it stays shareable without an 18+ gate on the homepage.

## FAQ

**What is Party Challenges?**
A free 18+ browser party card game with 1,000+ cards across 23+ themed decks. Dares, confessions, hot takes, and questions for friends, couples, and solo play.

**Who is it for?**
Friend groups at pregames and parties, couples on date nights, and solo players looking for reflection prompts or personal dares.

**Is it free?**
The core game is free with no account required. Premium unlocks additional 18+ content (After Dark decks and highest-intensity tiers).

**Why is it 18+?**
Multiple decks contain adult dares, explicit questions, and content not appropriate for minors. The age gate is enforced on entry.

**Do I need to download an app?**
No. Open [partychallenges.com](https://partychallenges.com) in any mobile browser and play immediately. You can optionally install it as a PWA from the home screen for faster loading and offline play.

**How many cards and decks are there?**
Over 1,000 cards across 23+ themed decks, with new decks added regularly.

**Does it work offline?**
Yes. After the first load, cards are cached locally and the game works without an internet connection.

---

*Build log by Inithouse. Party Challenges is live at [partychallenges.com](https://partychallenges.com).*
