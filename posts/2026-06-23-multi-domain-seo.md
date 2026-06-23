# Multi-domain SEO: how we run one product across five country TLDs

*Posted 2026-06-23*

[Živá Fotka](https://zivafotka.cz) runs as one product behind five separate domains: `.cz`, `.sk`, `.pl`, plus an English `.online`, plus a German `.de`. Same codebase, same backend, different markets. Search engines should hate this setup. In practice, it works — but it took a lot of getting wrong before it did.

Here's the playbook we'd hand to anyone considering the same path.

## Why not one domain with locale subfolders?

The Google-recommended way to do multi-language is `example.com/cz/`, `example.com/sk/`, etc. We tried that first. It performs worse than separate domains in markets where the local TLD signals trust. Czechs trust `.cz`. Slovaks trust `.sk`. Poles trust `.pl`. The local TLD is itself a ranking and conversion factor.

The cost of separate domains in 2026 is mostly an SEO complexity tax. You're managing five sets of Search Console properties, five sets of structured data, five sitemaps. If you're not willing to do that work, stay on subfolders. We did the work because the conversion difference was material.

## The setup

**One codebase, locale at the edge.** The site detects the domain at the CDN level and serves the right locale. Every page exists at the corresponding URL on every domain — `zivafotka.cz/about` and `zivafotka.sk/about` are different URLs serving different content, but the same codebase generated both.

**Hreflang done strictly.** Every page on every domain includes hreflang tags listing all language/region variants. We use the `x-default` attribute pointing to the English `.online` for unmatched regions. Done correctly, this tells Google "these pages are equivalents in different languages" and prevents them being treated as duplicates.

**Localized content, not translated content.** This was our biggest unlock. A literal translation of the Czech site into Polish ranked badly and converted worse. We had each market rewritten from scratch by someone fluent in that market — same brand, different voice. The Polish landing reads like a Polish company wrote it, not like a Czech company translated.

**Separate Search Console properties.** Each domain is its own property in GSC. We run a small dashboard that aggregates them, but we monitor each separately because the queries, click patterns, and CTRs are different per market.

## What we got wrong

**We initially shared canonical URLs across domains.** Don't do this. Each domain is its own site with its own canonicals pointing to itself. Cross-domain canonicals tell Google one of your sites is the "real" one and the others should be hidden.

**We didn't localize structured data immediately.** Schema.org metadata in the wrong language hurts. Google reads the language attribute and gets confused. Localize all structured data alongside the page copy.

**We ran identical ad creatives in different languages.** This is a separate problem from SEO but related. Translation doesn't carry tone. Each market needed creative variations that worked for *that* market's idiom and humor.

## What's working now

The strongest signal that the multi-domain setup is paying off: organic CTR on the local TLDs is significantly higher than on the English `.online` for queries that overlap. People click `.cz` over `.online` in CZ even when both appear in results. That's the trust signal you can't get from a subfolder.

We've also gotten ranking distinctions we wouldn't have on a single domain — the `.de` ranks well in Germany without competing for ranking space against the Czech version, because they're separate properties.

## The verdict

Multi-domain SEO is worth it if you have markets where local trust really matters and you're willing to do the operational work. It's not worth it if you're going to half-do it. The middle path — multi-domain with poor localization or shared canonicals — is worse than just running on a single international `.com`. Commit fully or stay subfolder.

— [Inithouse](https://inithouse.com)
