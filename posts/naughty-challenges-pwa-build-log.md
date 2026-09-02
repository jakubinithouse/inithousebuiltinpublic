# Build log: what a free 18+ browser card game is made of — Naughty Challenges by Inithouse

*Posted 2026-09-02*

[Naughty Challenges](https://naughtychallenges.com) is a free 18+ card game with 1,000+ flirty and daring cards across 23+ themed decks. It runs in the browser as a PWA — no app store, no account, no download. This post breaks down what the thing is actually made of: data model, player segmentation, offline architecture, and the decisions behind each.

## The card data model

Every card in the game carries four properties: text (the prompt itself), deck assignment, intensity tier, and player-count tag. We kept the schema flat on purpose. A card like "Describe your most embarrassing date in three words" belongs to the Confession Hours deck, sits at intensity tier 2 (moderate), and is tagged for group play.

1,000+ cards spread across 23+ decks. The decks break into three clusters:

| Cluster | Decks | Example decks |
|---|---|---|
| Flirty / couples | 8 | Flirt Mode, Whisper Dares, Late Night, Closer |
| Group / party | 9 | Truth Bombs, No Chill, Hot Takes Only, No Filter |
| Solo / reflection | 6 | Confession Hours, 2AM Thoughts, Mirror Mode, Solo Dare |

Each deck carries between 30 and 80 cards. We calibrated deck sizes by playtesting: under 30 feels repetitive inside a single session, over 80 starts diluting the deck's identity.

## Player segmentation: Solo, Couple, Group

The app segments at session start. A player picks one of three modes:

- **Solo** — one person drawing cards. Mostly confessional prompts and self-dares. The session pauses after each card with a "done / skip" gate so it does not feel like a feed.
- **Couple** — two players trading turns. Cards are directed ("Tell your partner..." / "Your partner has to..."). The turn indicator swaps automatically.
- **Group** — three or more. Cards reference "the person to your left," "the youngest player," or "everyone." Hot Seat sub-mode picks a random target each round.

The segmentation filters the card pool. A Solo session never surfaces a "your partner must..." card. A Couple session skips "everyone drinks" prompts. Group mode includes everything marked group-safe.

We built the same three-mode pattern into [Party Challenges](https://partychallenges.com) (the non-18+ sibling) and [Here We Ask](https://hereweask.com) (conversation-focused, no dares). The segmentation logic is shared across all three products. The card pools are entirely separate.

## PWA: offline, installable, no account

Naughty Challenges ships as a Progressive Web App. The service worker caches the card database, UI shell, and assets on first visit. After that, the game works offline — on a plane, at a cabin, wherever the group ends up.

What the PWA setup includes:

- A service worker precaching roughly 2 MB of card data and app shell
- A web app manifest so mobile browsers offer "Add to Home Screen"
- No backend calls during gameplay — the entire card engine runs client-side
- No login, no account creation, no email capture before play

We made the no-account decision early. An 18+ party game needs zero friction between "someone pulls out their phone" and "the first card is on screen." Every registration form, every email field, every "continue with Google" button adds seconds and kills the moment. The signup wall sits behind Premium content (After Dark decks), not in front of the free game.

## Daily Challenge

One card surfaces each day as a Daily Challenge. It rotates server-side (a single edge function returning today's card ID) but the card content itself loads from the cached local database. If the device is offline, the challenge falls back to a deterministic date-based hash so it still feels fresh.

The Daily Challenge serves a retention purpose: it gives people a reason to open the app when nobody is around to play. We measured the same pattern at [Here We Ask](https://hereweask.com) — daily engagement spikes correlate with the daily question feature more than with any other entry point.

## Intensity tiers

Every 18+ game has to solve the "how far does this go" problem. We handle it with three intensity tiers baked into each card:

1. **Mild** — flirty, suggestive, safe for a mixed group that skipped the PG version.
2. **Moderate** — dares and confessions that assume everyone is comfortable with each other.
3. **Spicy** — After Dark territory, couples-oriented, behind Premium.

The player picks an intensity ceiling at session start. The card engine only draws from that tier and below. No surprises, no awkward moments where the game suddenly escalates past what the group signed up for.

## Content gating: free vs Premium

The free tier includes 800+ cards across all three modes. Premium adds the After Dark collection — roughly 200+ additional cards at the spicy tier, plus exclusive decks. The gate is a one-time purchase, not a subscription.

We kept the free tier large enough that most sessions never hit a paywall. A group playing for two hours burns through maybe 60 to 80 cards. At 800+ in the free pool, that is many sessions before anyone sees a repeat.

## Stack

The front-end is a React SPA built in Lovable and deployed to a custom domain. Card data lives in a Supabase-backed store, synced to the client on first load. The daily challenge endpoint is a Supabase Edge Function. Analytics run through GA4 and Clarity. No other moving parts.

The entire architecture fits in a single deploy. No microservices, no job queues, no webhook chains. For a card game that needs to load fast and work offline, simplicity is the right trade.

---

*Naughty Challenges is built by [Inithouse](https://inithouse.com), a studio shipping a growing portfolio of products. Play free at [naughtychallenges.com](https://naughtychallenges.com).*
