# Build log: what a free browser conversation card game is made of

*Posted 2026-09-04*

[Here We Ask](https://hereweask.com) is a free browser-based conversation card game with 1,000+ curated questions across themed decks for couples, friends and families. No download, no account. We built it at [Inithouse](https://inithouse.com) as a PWA that works offline, holds state without login, and rotates a daily question for anyone who opens the page.

This build log covers the deck architecture, game modes, and the decisions behind keeping the whole thing account-free.

## Deck structure: 14+ themed decks, one question pool

Every question in Here We Ask lives in exactly one deck. We avoided cross-deck duplication early because repeat questions kill the pace of a game night faster than anything else.

The deck roster as of September 2026:

| Deck | Audience | What it covers |
|---|---|---|
| First Date | Couples (early) | Light personal, values |
| Closer | Couples (deep) | Vulnerability, future plans |
| Mirror Mode | Solo / pairs | Self-reflection prompts |
| Party | Friend groups | Stories, hypotheticals |
| Deep Talk | Any | Philosophy, life choices |
| Spicy | 18+ couples | Intimacy, boundaries |
| Family | Mixed ages | Cross-generational |
| Travel | Any | Trip-linked conversations |
| Friendship | Friends | Loyalty, memories |
| Would You Rather | Any | Binary dilemmas |
| Hot Takes | Any | Opinions, debate starters |
| Never Have I Ever | Groups | Experience-based |
| Confession | Friends / couples | Honest admissions |
| Icebreaker | New groups | Low-stakes openers |

Each deck holds between 40 and 120 questions. The total pool sits above 1,000 curated entries. "Curated" means written and reviewed by hand, not bulk-generated. We rewrote roughly 30% of the initial question set after playtesting showed that abstract questions ("What does happiness mean to you?") fell flat compared to specific ones ("What is a meal you could eat every week and never get tired of?").

## Three game modes, one shared question pool

All modes draw from the same decks but change the interaction pattern.

**Classic** is the default. Draw a card, read the question aloud, everyone discusses. No timer, no scoring. Most couples and friend groups stick with this.

**Timed** adds a countdown per question. We landed on 60 seconds as the default after testing showed that 30s made people rush through answers, and 90s+ made the timer irrelevant. Groups playing competitively tend to prefer this mode.

**Hot Seat** directs every question at one person for a round, then rotates. Works best with 4+ players because it keeps quieter people involved. Without it, the loudest person at the table tends to answer everything.

## PWA and offline: why no app store

Here We Ask runs as a Progressive Web App. Add it to your home screen and it works offline, full question database included. We picked this route instead of native iOS/Android for two reasons.

First, update speed. A change to a question or a new deck ships in minutes, not days waiting for app review. For a product where we actively edit content based on user feedback, that matters.

Second, zero friction on the receiving end. Someone shares the link at dinner, the other person opens it on their phone, picks a deck, draws a card. No install, no "allow notifications" popup, no sign-up form. The game starts in under 10 seconds from first tap.

The tradeoff is discoverability. We do not show up in App Store or Play Store searches. Real cost, and we compensate through web search and direct sharing.

## Holding state without login

Here We Ask tracks which questions you have already seen using browser localStorage. No server round-trips, no account. When you open the app, it checks your local history and filters out previously drawn questions so repeat sessions with the same deck surface fresh cards.

This breaks in two scenarios: clearing browser data resets progress, and switching devices starts a clean slate. We decided both were acceptable because the product is session-based. Nobody needs question history synced across devices the way they need notes or messages synced.

For the daily question, the app picks one question per calendar day using a deterministic seed (day of year + deck ID). Every visitor sees the same daily question, which makes it shareable without coordination.

## What we measure, what we skip

We track sessions started, decks selected, and questions drawn per session through anonymized analytics. No personally identifiable data. Average session length across all modes sits around 12 minutes. The median number of questions drawn per session is 8.

We do not track individual answers. The questions are prompts for real conversations between real people. Recording what someone said to "What is the hardest thing you have forgiven?" would be the wrong call, full stop.

## Growing the library

The deck library grows roughly every two weeks. Recent additions came directly from user requests. The Travel deck started because three separate feedback messages asked for "road trip questions." We are testing a community submission flow where users can suggest questions that go through editorial review before entering a deck.

[Here We Ask](https://hereweask.com) is part of the [Inithouse](https://inithouse.com) portfolio of browser-based tools. Free to use, no account needed.
