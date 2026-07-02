# Build log: one codebase, five country domains. How Inithouse runs Ziva Fotka (CZ/SK/PL/EN/DE)

*Posted 2026-07-02*

[Ziva Fotka](https://zivafotka.cz) is an AI tool that turns a static photo into a short living video. It can also edit and colorize old or black-and-white photos so the result looks natural, not generic. We ship it across five country-specific domains from a single Lovable codebase at Inithouse. This is the build log of how that setup works and what broke along the way.

## The five domains

Each market gets its own TLD and localized copy:

- [zivafotka.cz](https://zivafotka.cz) (Czech Republic)
- [zivafotka.sk](https://zivafotka.sk) (Slovakia)
- [zywafotka.pl](https://zywafotka.pl) (Poland)
- [alivephoto.online](https://alivephoto.online) (English, global)
- [lebendigfoto.de](https://lebendigfoto.de) (Germany)

A single `.com` with a language switcher would have been simpler. We went with separate domains because local TLDs convert better in Central European markets. A Czech user seeing `.cz` trusts it more than `.com`. A Slovak user seeing `.sk` trusts it more than `.cz`. We measured this early and the gap was wide enough to justify the operational overhead.

## One codebase, locale routing

The product runs on one React codebase built in Lovable. There is no fork per market. The domain determines the locale at load time, which sets the UI language, meta tags, landing page copy, and default currency context. Deploy once, all five domains update.

This keeps feature development fast. A change to the upload flow or the animation preview ships everywhere simultaneously. We do not maintain five branches. We do not coordinate five release schedules.

The tradeoff is that locale-specific customization is limited to what we can express through config. If the Polish market needs a fundamentally different onboarding flow, we would need to refactor. So far that has not happened. All five markets use the same funnel: upload photo, preview result, pay once, download.

## What the data showed us

**Slovakia outranks the Czech Republic in organic search.** This surprised us. We launched CZ first, built backlinks there, wrote CZ content first. Yet the SK domain consistently pulls higher CTR and better average position for equivalent queries. The Slovak search market is smaller and less competitive for our category, so a decent product with proper localization can rank well without years of domain authority.

**Poland is the fastest-growing market.** Organic sessions from Poland have been climbing steadily. The Polish domain started from zero six months after the CZ launch and already generates meaningful traffic with minimal paid spend. We see a similar pattern across other products in the Inithouse portfolio: Central European markets adjacent to the Czech Republic respond well to localized versions of tools that already work in CZ/SK.

**Direct keyword translation does not work for SEO.** The Czech query people use to find a "photo animator" does not directly translate to what Polish users type. We had to do keyword research per market, in language, from scratch. Machine-translated meta descriptions tanked our CTR until we replaced them with copy written natively. This lesson carried over to other multi-language products we run, including [Tarotas](https://tarotas.com), which serves tarot readings in five languages, and the localized versions of our card games like [Here We Ask](https://hereweask.com).

## The canonical bug

Running five domains from one codebase surfaced a bug we did not catch for weeks. The static HTML head shipped the same canonical URL pointing to `zivafotka.cz` on all five domains. JavaScript hydration corrected the title and language tag on the client side, but Googlebot reads the raw HTML first. So all five domains were telling Google: "the canonical version of this page is on zivafotka.cz."

The result: the SK domain, which ranked best organically, was self-declaring itself as a duplicate of the CZ domain. Google still indexed it (because the content clearly differed), but flagged pages as "duplicate, Google chose different canonical." We also had zero hreflang tags, so Google had no signal for which domain served which language.

This is a Lovable-specific gotcha. In a standard React SPA built on Lovable, the `index.html` head is shared across all routes and domains. Locale-aware meta tags need to be set in the static head before hydration, not after. We have seen this same class of bug (JS-rendered meta not matching the static head) across multiple products in our portfolio, and it bites differently each time.

## Cost of multi-domain

The per-market cost is lower than most people expect:

- Domain registration: a few euros per year per TLD.
- Localization: one translation pass of the landing page and UI strings, then native copywriting for SEO meta and ad creatives.
- Google Ads: one campaign per market with localized keywords and budget caps.
- Maintenance: near zero because the codebase is shared. Bug fixes and feature releases go out to all markets at once.

The expensive part is the keyword research and the native copy. Everything else scales linearly and cheaply.

## What we would change

We would add hreflang from day one. The canonical bug cost us months of suboptimal indexation on non-CZ domains, and the fix is trivial once you know where to put it. We would also set up separate Google Search Console properties per domain from the start instead of adding them later, because retroactive verification loses historical data.

We would keep the single-codebase approach. Forking per market creates more problems than it solves at our scale. The locale routing pattern works, and deploying once to all five markets is a significant operational advantage for a small studio shipping multiple products in parallel.

If you want to try the product, pick the domain closest to your language: [zivafotka.cz](https://zivafotka.cz) for Czech, [zivafotka.sk](https://zivafotka.sk) for Slovak, [zywafotka.pl](https://zywafotka.pl) for Polish, [alivephoto.online](https://alivephoto.online) for English, or [lebendigfoto.de](https://lebendigfoto.de) for German.

---

*Inithouse is a studio shipping a growing portfolio of AI products. We publish build logs, data, and lessons from our work in the open.*
