# Portfolio retro: what four card games taught Inithouse about PWA and no-account play

*Posted 2026-07-03*

At Inithouse we ship browser-first products. No app stores, no mandatory sign-ups, no install friction. Over the past year we built four card games on top of the same progressive web app architecture, and each one taught us something the previous one missed.

This is a retro on what worked, what broke, and what we would do differently.

## The four games

The card-game cluster at Inithouse currently includes:

- [Party Challenges](https://partychallenges.com): an 18+ party card game with 1,000+ cards across 23+ decks (confessions, dares, hot takes). For friend groups, couples, and solo players.
- [Scary Challenges](https://scarychallenges.com): a horror-themed fork of the same engine. Campfire stories, dares for sleepovers, dark confessions.
- [Naughty Challenges](https://naughtychallenges.com): the explicit tier. Couples, friends, solo players at 2 AM pulling cards from After Dark decks.
- [Here We Ask](https://hereweask.com): a conversation card game with curated questions in themed decks (couples, friends, family, deep). Lighter in tone, broader in audience.

All four run as PWAs. One person opens the URL on their phone, the group plays off that single screen. Nobody downloads anything.

## Lesson 1: no-account play changes how people find you

We made sign-up optional from the start. A group at a party does not want to create four accounts at 11 PM. So the default flow is: open the link, pick a deck, play.

This turned out to matter for distribution more than we expected. When someone texts a link to a friend, the friend taps it and is playing within seconds. There is no "download and create an account" wall where half the group drops off. The URL itself is the entire onboarding.

The tradeoff is real, though. Without accounts, tracking returning users relies on browser storage, which clears. We can see session counts but struggle to distinguish "10 people played once" from "2 people played five times." That blind spot shaped how we think about retention signals in this cluster.

## Lesson 2: forking a product beats adding a mode

Party Challenges started as one game with every kind of card in it. When we wanted to add horror content, the first instinct was to make a "Scary Mode" toggle inside the existing app.

We tried it. It felt wrong. The brand of an 18+ party game and the brand of a horror dare game pull in different directions. The audiences overlap but they search for different things and share links in different contexts.

So we forked. Scary Challenges got its own domain, its own visual identity, its own card library. The codebase is shared (same Lovable project architecture, same Supabase backend pattern), but the product surface is independent.

The result: Scary Challenges found its niche faster than it would have as a feature inside Party Challenges. Horror fans searching for "scary dare games" land on a product that matches their intent exactly, not on a party game that also has some spooky cards.

We repeated the pattern with Naughty Challenges. Same architecture, different positioning, separate domain.

## Lesson 3: card length matters more than card count

Early on we chased card volume. More cards meant more variety, which seemed like an obvious good. We crossed 1,000 cards per game and kept writing.

What actually correlated with longer sessions was card length. Cards in the 8 to 12 word range got read aloud quickly, produced a reaction, and moved the game forward. Longer cards (20+ words) stalled the pace. People would read them silently, then paraphrase, and the group energy dipped.

We went back and edited. Shorter, punchier cards. The total count barely changed, but the play experience tightened up.

## Lesson 4: PWA "install" is underrated

Most of our players never install the PWA. They open the URL in their mobile browser and play. That is fine. But the subset who do tap "Add to Home Screen" behave very differently. They come back more often, and their sessions run longer.

We did not push the install prompt aggressively because interrupting someone mid-game with a banner felt wrong. Instead, we surface it after a session ends: "Add to home screen for faster access next time." Gentle, post-value, no pop-up during play.

This small change moved the install rate enough to matter. And installed PWA users became our most reliable returning cohort across all four games.

## Lesson 5: shared architecture, separate identity

The four games share a codebase, a backend pattern, and a deployment pipeline. This saves us enormous time when shipping updates. A bug fix in the card rendering logic rolls out to all four games in one deploy cycle.

But the products never reference each other. Party Challenges does not say "from the makers of Scary Challenges." Each game stands on its own domain, with its own name, its own deck themes, its own color palette.

This was a deliberate choice. Cross-promotion between products in the same cluster tends to confuse more than it helps, especially when the audiences overlap but the positioning diverges. A horror fan does not need to know that the same studio also makes a couples card game. They need the horror game to feel like it was built for them.

## What we would do differently

Start with the fork model from day one. The time we spent building and then unbundling "modes" inside Party Challenges was wasted effort. If we had launched each game as a separate product from the start, we would have saved weeks.

We would also invest in a shared card authoring tool earlier. Right now, writing and tagging 1,000+ cards per game is manual. A structured editor with category/intensity metadata built in would cut the content creation time significantly.

## Where this sits

Inithouse ships products across several categories, not just games. But the card-game cluster taught us patterns that apply to the rest of the portfolio: PWA-first distribution, no-account defaults, product forking over feature stacking. Those principles now show up in everything we build.

The four games are live. Try any of them from your phone, no download needed.
