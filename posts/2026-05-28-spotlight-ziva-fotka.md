# Spotlight: Živá Fotka. One codebase, five domains, lessons in multi-market launch

*Posted 2026-05-28*

[Živá Fotka](https://zivafotka.cz) turns still photos into short animated portraits. Upload a face, get back a five-second loop where the subject blinks, smiles, looks around. It sounds gimmicky until people upload photos of relatives who passed away years ago. Then it stops being gimmicky.

Behind the simple landing page is something most studios our size don't attempt: one codebase serving five markets through five separate domains.

- 🇨🇿 [zivafotka.cz](https://zivafotka.cz)
- 🇸🇰 [zivafotka.sk](https://zivafotka.sk)
- 🇵🇱 [zywafotka.pl](https://zywafotka.pl)
- 🇬🇧 [alivephoto.online](https://alivephoto.online)
- 🇩🇪 [lebendigfoto.de](https://lebendigfoto.de)

## Why five domains for one product?

The instinct is to launch on `.com` and call it global. We tried that. The conversion on local-language landing pages with a local TLD beat the `.com` translation by a wide margin in every market we tested. Trust is local. People in Slovakia don't fully trust `.cz`. People in Poland definitely don't. So we run the same product behind separate domains, each properly localized.

The cost of doing this in 2026 is much lower than it used to be. Localization is a translation pass, then SEO meta, then a Google Ads campaign tuned to the market. The hard part is resisting the urge to fork the codebase. One codebase, locale-aware everything, deploy once.

## What we learned

**CTR varies wildly by market.** The same creative, same landing, different language: 4x difference in click-through between the best and worst market. We assumed the product was the thing. The product is half the thing. The market is the other half. We saw a similar pattern with [Here We Ask](https://hereweask.com), our conversation card game; the English version performs differently from the base even though the game mechanics are identical.

**Search behavior is not symmetric.** What people google in Czech to find a "photo animator" doesn't translate to what they google in Polish. Direct keyword translation gave us terrible match rates. We had to do keyword research market by market, in language, the slow way.

**Localization beats translation.** A literal translation of marketing copy reads stiff. We've had people in each market rewrite landing pages in the natural voice of the language. The conversion bump from that alone was worth the friction. This lesson carried over to [Tarotas](https://tarotas.com), our tarot app serving 78 cards in five languages on a single domain; the copy there needed the same per-language care.

## What we'd do differently

We launched all five markets within a month of each other. In hindsight, we'd stagger them. Each new market reveals something (a pricing assumption, a payment provider issue, a translated word that means something unfortunate in another language) and rolling out one market at a time would have let us learn from each launch before paying for the next one.

Multi-domain is harder than it looks, but cheaper than the alternative, which is "build separate products per market." Worth doing, once you've earned the right to.

// The Inithouse crew
