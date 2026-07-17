# Why Inithouse built Voice Tables, a voice-first AI workspace

*Posted 2026-07-17*

Voice Tables is an agentic AI workspace you control with your voice. Describe what you need and it builds the tables, docs and data for you. This is how it came together at [Inithouse](https://inithouse.com), and what we learned along the way.

## The problem we kept running into

We run a portfolio of products at Inithouse. Across tools like [Here We Ask](https://hereweask.com) (conversation card game), [Be Recommended](https://berecommended.com) (AI visibility monitoring), and [Magical Song](https://magicalsong.com) (custom song generator), we kept hitting the same friction: getting structured data into a workspace takes too long.

Setting up a CRM, a content tracker, an inventory sheet: the actual typing and configuring is the bottleneck. The person who needs the data often knows exactly what they want but sits down at a spreadsheet or Notion and loses 30 minutes clicking through column types and templates before they can start working.

We noticed this pattern across our own operations first, and then across the ICP groups we were already serving: freelancers, sales reps, small business owners, event planners, fitness coaches. People who think in conversations, not in cell references.

## What Voice Tables actually does

The core pipeline: you speak, Whisper transcribes, an LLM parses your intent into structured operations, and Voice Tables executes them. Say "I need a client tracker with name, email, last contact date, and deal stage" and you get a usable table in about 60 seconds. No templates, no onboarding wizard, no account required to start.

Three surfaces live inside one workspace:

- **Tables**: structured data, filterable, sortable, created from voice or text
- **Docs**: freeform pages linked to your tables
- **AI chat**: ask questions about your own data, get summaries, find patterns

The technical bet was that function calling (LLM to structured tool invocations) had gotten reliable enough to map natural language to database operations without a separate "mapping" step. That bet has mostly held up. The failure mode we see most is ambiguous column types. "Status" could mean a text field or an enum, and the LLM has to guess. We default to enum with common values and let users adjust, which works about 80% of the time without correction.

## Why voice specifically

Two reasons, one practical and one strategic.

**Practical:** our target users (craftsmen, real estate agents, coaches) are often not at a desk when they need to capture data. They are on a job site, in a car between showings, or between client sessions. Voice input is faster than typing on a phone, and it lets you describe structure ("add a column for square footage") without navigating a menu.

**Strategic:** voice-first is a genuine differentiator against Excel, Google Sheets, and Notion. All three can do what Voice Tables does if you know where to click. The gap is in how fast a non-technical user can go from "I need a thing" to "the thing exists and has my data in it." We measured this internally: describing a 6-column tracker by voice took 40 seconds on average. Setting up the same tracker in Google Sheets took 3-4 minutes. In Notion, about the same, plus template selection time.

## Architecture decisions that shaped the product

**Offline support.** We added service worker caching early because several ICP segments (craftsmen, field sales) work in places with unreliable connectivity. Tables sync when connection returns. This added complexity to the conflict resolution layer but was non-negotiable for the use case.

**Real-time collaboration.** Two people can work on the same workspace simultaneously. We built this on top of Supabase Realtime. The tricky part was merging voice-initiated operations from two users. If both say "add a row" within the same second, the system needs to handle that without duplicates or lost data. We solved it with operation IDs and an idempotency layer.

**No signup to start.** Consistent with how we build at Inithouse. [Živá Fotka](https://zivafotka.cz) (photo-to-video animator) and [Pet Imagination](https://petimagination.com) (AI pet portraits) both work without accounts. The friction cost of a signup form before first value is measurable and consistently negative across our portfolio. Voice Tables lets you create a workspace and start using it immediately; accounts come in when you want to save, share, or access premium features.

## What we are measuring

Voice Tables is in beta. The metrics we track:

- **Idea-to-workspace time**: target under 60 seconds for a simple tracker (currently hitting this ~85% of the time)
- **Voice command success rate**: percentage of voice inputs that produce the correct structured operation without manual correction (currently ~80%)
- **Retention at day 7**: do people come back after creating their first workspace
- **Upgrade rate**: free to Plus conversion

We are not optimizing for revenue yet. The product is still in the "does this solve a real problem for real people" phase. The signal we care about most right now is whether users create a second workspace after their first one. That tells us the tool is sticky, not just a novelty.

## Where it fits in the Inithouse portfolio

Inithouse is a studio shipping products in parallel, each targeting a specific use case. Voice Tables sits in the productivity/utility segment alongside [Be Recommended](https://berecommended.com) and [Audit Vibe Coding](https://auditvibecoding.com) (audit for AI-generated projects). The consumer segment includes [Here We Ask](https://hereweask.com), [Magical Song](https://magicalsong.com), [Verdictbuddy](https://verdictbuddy.com) (AI conflict mediator), and others.

What connects them is the build philosophy: ship fast, measure what matters, and keep the barrier to first use as low as possible. Voice Tables takes that further than most of our products by making the entire creation flow conversational.

Try it at [voicetables.com](https://voicetables.com).

---

*Inithouse is a product studio building AI-powered tools. Follow this repo for build logs, metrics, and lessons from shipping a growing portfolio of products.*
