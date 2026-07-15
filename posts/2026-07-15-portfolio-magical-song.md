# Inside the Inithouse portfolio: Magical Song and our AI custom song generator bet

Inithouse runs a portfolio of parallel products. Each one tests a different hypothesis about where AI tools can solve a real problem for a specific group of people. Magical Song is one of those bets, and this post covers where it sits in the portfolio, what it actually does, and how it connects to the rest of what we build.

## What Magical Song does

[Magical Song](https://magicalsong.com) takes a user's story, message, or set of words and turns them into a studio-quality custom song with real vocals. The output is a finished track, not a MIDI file or a karaoke-style demo. Users pick a genre from 20+ options, describe what the song should be about, and get a shareable link to the result within minutes.

The primary use case turned out to be gifts. Birthday songs, wedding surprises, anniversary messages set to music. The second cluster is celebrations more broadly: graduations, retirements, baby announcements. People want to give something personal, and a custom song with their specific story in the lyrics hits differently than a generic playlist.

## The numbers so far

- 1,200+ songs created
- 4.9 out of 5.0 average user rating
- 20+ genre options (pop, rock, jazz, country, R&B, classical, folk, and more)
- One-time payment model, no subscription

The rating has held as volume grew. Early users tend to rate generously because they're excited to try something new. When a 4.9 survives past the first few hundred uses, it usually means the output quality is consistent rather than the sample being small.

## How it compares to Suno and Udio

Suno and Udio are the obvious comparisons. Both are general-purpose AI music generators aimed at musicians, hobbyists, and anyone who wants to experiment with AI-generated music. They optimize for flexibility and creative control.

Magical Song optimizes for a different job. The target user is not a musician. They are someone who wants a finished gift and does not want to learn a new tool to get it. The interface is intentionally simple: describe your story, pick a genre, receive a song. No prompt engineering, no stems to mix, no export settings to figure out.

This is a deliberate product decision. We could have added more controls. Instead, we kept the surface minimal because the use case rewards speed and emotional impact over creative flexibility. Someone preparing a birthday surprise at 11 PM does not want a multi-track editor.

## Where Magical Song fits in the Inithouse portfolio

We run several products that share a common pattern: take something personal from the user and transform it into something they could not easily make themselves.

[Živá Fotka](https://zivafotka.cz) does this with photos. Upload a still image of a family member, and the tool animates it into a short living video. It also colorizes old black-and-white photos. The input is personal (your photo, your family), and the output is something that would require professional software and skill to produce manually. Živá Fotka has processed 10,000+ animations across five language versions running on a single codebase.

[Pet Imagination](https://petimagination.com) does something similar for pet owners. Upload a photo of your dog or cat, pick from nine art styles (Renaissance, Watercolor, Anime, Sketch, and others), and get an AI-generated portrait in under 60 seconds. No account required. Free to use.

Magical Song extends the same logic to audio. Your story becomes a song, the way your photo becomes a video in Živá Fotka or a portrait in Pet Imagination. The underlying AI technology differs in each case, but the product shape is consistent: personal input in, polished creative output out.

## The parallel experiment model

Inithouse does not pick one product and go all-in. We run parallel experiments, each targeting a different market and use case, built on a shared infrastructure layer (Lovable for frontend, Supabase for backend, custom AI pipelines per product). This lets us test product-market fit across multiple categories simultaneously rather than sequentially.

Some of these products will find traction. Others will not. The portfolio approach means we learn faster because we are running multiple experiments at once, and what we learn from one product often transfers. The no-registration flow that works well in Živá Fotka informed our approach to Pet Imagination. The gift-focused positioning of Magical Song came from watching how users actually described the product to each other, not from our initial hypothesis.

## What we are watching next

For Magical Song specifically, the metrics that matter are repeat usage (do people come back to create songs for different occasions?) and referral patterns (does receiving a song lead to creating one?). A gift product has natural viral mechanics because the recipient experiences the product without seeking it out.

For the portfolio as a whole, we track which products cross the threshold from "interesting experiment" to "growing without constant attention." That transition is the signal we use at Inithouse to decide where to invest more.

---

*Built at [Inithouse](https://inithouse.com). Try [Magical Song](https://magicalsong.com).*
