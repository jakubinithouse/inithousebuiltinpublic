# One codebase, four card games: how Here We Ask anchors the Inithouse card-game cluster

*Posted 2026-07-25*

We ship a lot of small products at [Inithouse](https://inithouse.com). Most of them are independent experiments: different categories, different audiences, different tech stacks. But four of our games share a single codebase, and that decision has shaped how we build, test and extend all of them.

The anchor product is [Here We Ask](https://hereweask.com), a free browser-based conversation card game with 1,000+ curated questions across themed decks for couples, friends and families. No download, no account, just pick a deck and start talking. It runs as a PWA, works offline, and the whole experience loads in a few seconds on a phone.

When the core was solid enough, we forked it three times.

## The cluster

[Party Challenges](https://partychallenges.com) is the rowdy sibling: 1,000+ cards across 23+ decks covering confessions, dares, hot takes and an After Dark tier. Same deck engine, same Hot Seat and No Hesitation modes, same PWA shell. Different tone entirely. Where Here We Ask nudges people toward honest conversation, Party Challenges nudges them toward chaos.

[Scary Challenges](https://scarychallenges.com) took the same skeleton and wrapped it in horror art direction. Campfire decks, dare cards designed for sleepovers, an atmosphere that actually makes people uncomfortable in a fun way. The card engine did not change. The intensity system and the visual language did.

[Naughty Challenges](https://naughtychallenges.com) rounds out the set: flirty, spicy, couples-oriented. Same 1,000+ cards structure, same game modes, same free-plus-premium model. A completely different emotional register.

Four games. One deck engine. One PWA runtime. One deployment pipeline.

## What the shared core actually is

The codebase handles deck loading, card sequencing, game mode logic (Classic, Timed, Hot Seat, No Hesitation, Spin It), offline storage, daily question rotation and the premium gate. None of that changes between products. When we fix a bug in the card sequencer, it ships to all four. When we add a game mode, it becomes available across the cluster.

The content layer sits on top: themed decks, card copy, intensity ratings, unlock tiers. Each product has its own content library, its own art, its own brand personality. The engine does not care whether the card says "What would you do if you won the lottery?" or "Describe your most embarrassing dare in one sentence." It draws, sequences and presents.

This split saved us months. Building a card game from scratch is maybe two weeks of focused work. Building four independent card games with four independent code paths would have been eight weeks plus ongoing maintenance across four repositories. Instead, we maintain one, and the per-product work is mostly editorial: writing cards, choosing decks, setting the tone.

## Why four games instead of one

We considered a single app with switchable themes. A toggle that turns Here We Ask from "heartfelt couples questions" into "horror sleepover dares." On paper it sounds cleaner. In practice, it confused everyone who tested it.

People search for specific things. Someone looking for a horror party game does not want to land on a page full of relationship questions and then find the horror toggle in settings. They want a product that looks, feels and sounds like what they searched for. The homepage, the copy, the decks visible before you even start playing should all signal the same thing.

Separate domains let each product own its category. Scary Challenges can rank for horror card game queries without diluting Here We Ask's positioning around couples and conversation starters. The SEO footprint is four sites, each tight on its topic, instead of one site trying to span every mood.

The trade-off is real: four domains to manage, four sets of metadata, four content libraries to keep current. But the shared engine means "manage" mostly equals "deploy once and write cards."

## What we actually learned

A few things stood out after running the cluster for a couple of months.

Intensity configuration matters more than we expected. Here We Ask has no intensity system because its cards are conversation starters, not challenges. The other three needed fine-grained intensity levels so that a casual group and a rowdy group could have different experiences with the same deck. We built it once, but calibrating it per product took more editorial time than writing the cards themselves.

Retention hooks diverge even when the engine is shared. Daily questions work well for Here We Ask (people come back for a new conversation prompt). Daily dares work differently for Party Challenges (people come back when they have a group to play with, not daily). Same feature, different user behavior, and we only saw it in the data after launch.

Content velocity scales. With one engine and four editorial pipelines, we can publish new decks across the cluster faster than we could ship features on a single product. The bottleneck shifted from engineering to writing, which is exactly where we wanted it for a card game portfolio.

## Where this stands now

At Inithouse, we treat the card-game cluster as one unit with four faces. Engineering improvements flow to all four. Content stays independent. Each product builds its own audience while sharing the underlying reliability of a single, well-tested PWA runtime.

The bet is simple: if one of the four finds strong traction, the others benefit from every engine improvement made along the way. If none of them do, we learned the lesson once instead of four times.
