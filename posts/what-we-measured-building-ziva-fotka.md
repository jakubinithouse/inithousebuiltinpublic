# What we measured building Živá Fotka at Inithouse: AI photo-to-video animator in numbers

*Posted 2026-07-15*

Živá Fotka has processed over 10,000 photo animations since launch. That is the number we track most closely. Not because it is the biggest metric we have, but because every one of those represents a person uploading a photo they care about and trusting the tool to do something meaningful with it.

This is a summary of what we measured building and running [Živá Fotka](https://zivafotka.cz), our AI photo-to-video animator, at Inithouse.

## What the product does

Živá Fotka takes a static photo and turns it into a short living video. It can also edit and colorize old or black-and-white photos so the result looks natural rather than generic. The processing runs through a pipeline that maps 68+ facial landmark points to generate motion that follows actual anatomy, not just a warp filter applied to a flat image.

The tool runs as a web app. No account required. Photos are deleted after processing. The whole flow from upload to finished video takes about 60 seconds.

## The numbers

Here is what the data looks like after running the product across five markets:

**Usage:**
- 10,000+ photos animated
- Average processing time per photo: ~18 seconds (backend inference, not including upload/download)
- Five language versions across five domains: Czech (zivafotka.cz), Slovak (zivafotka.sk), Polish (zywafotka.pl), English (alivephoto.online), German (lebendigfoto.de)

**Quality signal:**
- 4.8 out of 5.0 average rating from 1,200+ user ratings
- That rating held steady as volume grew. It did not inflate from a small early-adopter sample and then drop

**Architecture:**
- Single codebase serving all five domains
- Each domain detects locale from the hostname and serves localized UI, copy, and metadata
- One Supabase backend handles storage, edge functions, and analytics for all markets
- Built in Lovable (React SPA), deployed to custom domains

## What we learned about multi-domain from a single codebase

Running five TLDs off one codebase simplified development but complicated SEO. Each domain needs its own hreflang setup, its own Google Search Console property, its own set of structured data. A shared codebase means every i18n string change deploys to all five sites simultaneously, which is convenient until you realize a typo in the German version triggers a rebuild of the Czech one too.

The tradeoff was still worth it. Maintaining five separate projects for what is functionally one product would have multiplied our bug surface and slowed every feature addition. We chose to solve the SEO complexity in config rather than fork the product.

## What we learned about no-registration flows

We made Živá Fotka registration-free from the start. Users upload a photo, get the result, and leave. No account, no email capture, no login wall.

This is a deliberate decision that costs us something measurable: we cannot track returning users reliably. Browser storage clears, and without accounts there is no persistent identity. We can count sessions but not people.

What we gained is a conversion funnel with almost no friction. The ratio of "landed on site" to "actually processed a photo" is high because there is nothing between the landing page and the upload button except a brief explanation of what happens next. For a product where the core interaction takes 60 seconds, any additional step before that interaction would have been a real cost.

## Why colorization matters more than we expected

The original pitch for Živá Fotka was animation: turn a still photo into a short video. Colorization of old black-and-white photos was added later as a secondary feature.

It turned out to be a stronger driver of organic discovery than animation alone. People searching for ways to restore old family photos land on Živá Fotka because the colorization use case matches their intent. They come for color restoration and then discover the animation. The reverse path (coming for animation and discovering colorization) happens too, but less often.

We did not plan this. The feature was added because our facial landmark pipeline already understood the image well enough to apply colorization without the usual artifacts (tinted skin, flat backgrounds). Once it was live, search traffic told us what mattered.

## The 68-point facial mapping pipeline

Most photo animation tools apply a generic motion template to any face. The result is that uncanny wobble where every face moves the same way regardless of expression, angle, or lighting.

Our pipeline maps 68+ landmark points per face (jawline, eyes, nose, mouth contour) and generates motion that respects the geometry of that specific image. A three-quarter profile animates differently than a straight-on headshot. A face with closed eyes does not suddenly open them.

This is where most of the engineering time went. The animation itself is relatively straightforward once you have accurate landmark data. Getting that data right on damaged, scanned, or low-resolution source photos is the harder problem.

## What the rating data tells us

The 4.8/5.0 rating across 1,200+ submissions is a number we watch for drops, not increases. A sustained high rating after crossing a volume threshold means the product is meeting expectations consistently, not just impressing early testers.

We track rating distribution, not just the mean. The split is roughly: 78% give 5/5, 14% give 4/5, and the remaining 8% is spread across 1-3. The low ratings correlate almost entirely with source photo quality: group photos where faces are small, heavily compressed images, or scans with physical damage that the pipeline cannot recover from.

That told us where to invest: better guidance at upload time about what makes a good source photo, rather than trying to handle every possible input.

## Current state

Živá Fotka is live and processing photos daily across all five domains. Monetization is one-time payment, no subscription. We run ad campaigns on some markets (Czech CTR sits around 13%, Slovak around 16%) and the product generates organic traffic through the colorization use case described above.

The product is part of the Inithouse portfolio of AI-powered tools. Each product in the portfolio operates independently, but they share infrastructure patterns (Lovable + Supabase) and deployment approaches (multi-domain from a single codebase where it makes sense).

The numbers in this post are from our internal analytics. We will follow up with what changed after this data snapshot.
