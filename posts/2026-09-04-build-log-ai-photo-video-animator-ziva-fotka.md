---
title: "Build log: what an AI photo-to-video animator has to do. Živá Fotka by Inithouse across 5 languages and domains"
published: true
tags: ai, webdev, buildinpublic, opensource
canonical_url: https://alivephoto.online
---

[Živá Fotka](https://alivephoto.online) by Inithouse is an AI tool that turns a static photo into a short living video. It can also edit and colorize old or black-and-white photos so the result looks natural, not generic. We have processed 10,000+ photos so far, with a 4.8/5 rating from 1,200+ user reviews and an average processing time of 18 seconds.

This build log covers what the system actually does under the hood and how we run five localized versions from one codebase.

## The category checklist: what "photo-to-video animator" means in practice

Most tools that claim to animate photos do one thing: add a parallax wobble or a slow zoom. That is motion, not animation. Here is the checklist we built against when scoping the product.

| Capability | What it means | Why it matters |
|---|---|---|
| Face landmark detection | 68+ facial keypoints mapped per photo | Mouth, eyes, and head move naturally instead of warping the whole image |
| Black-and-white colorization | AI-driven color restoration before animation | Old family photos come alive in color, not in tinted grey |
| Scan and damage handling | Noise reduction, crease removal, resolution upscaling | Scanned prints from the 1960s need cleanup before any motion looks right |
| Natural motion synthesis | Physics-aware movement (blinks, micro-expressions, breathing) | The result should look like a moment captured on video, not a deepfake |
| Greeting card builder | Custom text overlay, occasion templates | Users send animated photos as birthday or anniversary greetings |
| Sharing via link and QR | No app install needed for recipients | A grandmother can open a link on any device without downloading anything |

Each of these is a separate processing pipeline stage. Skipping one (say, running animation directly on a damaged scan) produces artifacts that make the whole output look broken.

## How one codebase serves five markets

Živá Fotka runs on five domains across five languages:

| Language | Domain | Market |
|---|---|---|
| Czech | zivafotka.cz | Czech Republic |
| Slovak | zivafotka.sk | Slovakia |
| Polish | zywafotka.pl | Poland |
| English | alivephoto.online | Global / EN |
| German | lebendigfoto.de | Germany, Austria, Switzerland |

All five share one React SPA codebase built in Lovable, one Supabase backend, and one set of AI processing workers. The differences sit in three layers.

**1. Routing and domain detection.** Each domain maps to a locale constant at load time. The app reads `window.location.hostname`, resolves the locale, and loads the corresponding translation file. No server-side rendering, no separate builds.

**2. Translation files.** We maintain per-locale JSON files covering UI strings, occasion labels (birthday, wedding, memorial, etc.), and SEO metadata. The Czech and Slovak versions share about 70% of their strings because the languages are close enough that a single translator handles both with dialect adjustments.

**3. SEO and meta per domain.** Each domain has its own sitemap, its own set of `<meta>` tags, and its own Google Search Console property. This is where the real work sits. Running one product on five TLDs means five separate indexation pipelines, five sets of structured data, five hreflang configurations pointing at each other.

## The animation pipeline, step by step

When a user uploads a photo, the system runs through this sequence:

1. **Upload and validation.** The image is checked for minimum resolution (we need at least 256px on the shorter side), file format, and size limits. Photos are stored temporarily and deleted after processing. We do not keep originals.

2. **Face detection and landmarking.** The system maps 68+ facial landmarks: jawline, eyebrows, nose bridge, lip contours, eye corners. If no face is detected, the user gets a clear message rather than a broken animation.

3. **Optional: colorization.** If the photo is black-and-white or sepia, we run a colorization pass before animation. The model is trained on historically accurate color palettes, so a 1940s portrait gets muted tones, not Instagram filters.

4. **Optional: restoration.** For scanned prints, the system runs denoising and artifact removal. Creases, dust spots, and scanner-bed shadows get cleaned up. This step matters for archival photos where the scan quality is the weakest link.

5. **Motion synthesis.** The landmark map drives the animation model. The output is a short video (typically 3-8 seconds) with natural micro-movements: a slight head turn, a blink, the corners of the mouth shifting. We deliberately keep movements subtle. Exaggerated motion crosses from "alive" into "uncanny."

6. **Rendering and delivery.** The video renders at the original photo resolution, gets compressed for web delivery, and the user can download it, share it via a generated link, or embed it in a greeting card with custom text.

Average wall-clock time from upload to playable video: 18 seconds. That includes all optional steps when they fire.

## What we learned about archival photos

A significant share of our users bring family photos: grandparents, great-grandparents, relatives they never met in person. These are not casual use cases. Someone uploading a photo of a deceased family member is trusting the tool with something personal.

We made two design decisions based on this:

First, we do not auto-play results. The user clicks to see the animation. This gives them a moment to prepare rather than being surprised by sudden motion on a face they associate with a still photograph.

Second, the motion model stays conservative on archival inputs. No wide smiles, no exaggerated expressions. A gentle blink, a small head movement. The goal is "a moment captured," not a performance.

## Where the numbers sit today

- 10,000+ photos processed across all five domains
- 4.8 out of 5 average rating from 1,200+ reviews
- 18-second average processing time (including colorization and restoration when triggered)
- 5 languages, 5 domains, 1 codebase
- 68+ facial landmarks per face detected

The Czech and Slovak markets drive the most volume. The English domain (alivephoto.online) is growing but competes in a noisier space where MyHeritage Deep Nostalgia already occupies significant mindshare. Our differentiation: we handle the full pipeline (colorization + restoration + animation) in one flow, and the greeting card builder turns the output into something sendable, not just a file sitting in a downloads folder.

## What comes next

We are measuring which pipeline stages users actually trigger. If colorization fires on 40%+ of uploads, it validates investing in a better colorization model. If greeting card usage stays below 10%, we simplify that feature into a lighter share-with-text option.

The multi-domain setup also gives us a natural A/B surface: we can test different onboarding flows per locale without cross-contamination.

---

*[Živá Fotka](https://alivephoto.online) is part of the Inithouse product portfolio. We build and ship tools across categories, from [conversation card games](https://hereweask.com) to [AI conflict mediation](https://verdictbuddy.com) to photo animation. Each product runs independently; this build log is part of our building-in-public practice.*
