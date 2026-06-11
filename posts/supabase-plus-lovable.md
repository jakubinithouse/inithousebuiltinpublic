# Supabase + Lovable: How Inithouse Ships a Growing Portfolio of MVPs on One Stack

*Posted 2026-06-11*

At Inithouse, a studio shipping a growing portfolio of products in parallel, every new product starts with the same two tools: [Lovable](https://lovable.dev) and [Supabase](https://supabase.com). We wrote about [why we use Lovable](./why-we-use-lovable.md) already. This post is about the other half of the stack.

## Why Supabase specifically

The pitch for Supabase is usually "Postgres with auth and storage." That's accurate but misses what makes it useful in a portfolio context where we spin up new products regularly.

**Edge Functions in TypeScript.** We can write a server endpoint in the same file structure as the frontend, deploy it to the same project, and call it from the Lovable app without leaving the editor. For MVPs where the backend is "validate this, call an API, store the result," this covers the entire stack. At [Magical Song](https://magicalsong.com), our custom song generator, the whole payment and generation pipeline runs through Edge Functions.

**Row-Level Security gives you multi-tenant for free.** Most of our products have user accounts. Configuring RLS once on a table and trusting it to enforce per-user data access removes the most error-prone code from the app. We have never had a data leak between users on a product using RLS correctly. We have had multiple close calls on products where we tried to do auth checks at the app layer instead.

**The dashboard is fast.** Not a real technical argument, but it changes how we work. When we can poke at data in the Supabase UI without writing a query, we debug faster, we make decisions faster, we don't accumulate that "I'll look into it later" backlog of suspicious user reports. At [Watching Agents](https://watchingagents.com), where AI agents track hypotheses in real time, being able to inspect the evidence table mid-run has saved us from shipping broken agent logic more than once.

## What Lovable adds to this picture

Lovable scaffolds against a Supabase project natively. It reads the schema, generates typed queries, handles auth flows. The combination means going from "I have an idea" to "I have a working logged-in app that stores user data" is a same-day exercise.

The closest comparison is Firebase plus your frontend of choice. We have used Firebase. The reason we switched is not ideology; it is that Supabase is Postgres. When a product gets traction and starts asking real questions of its data (cohort analysis, retention curves, custom reports), Postgres lets us do that without rebuilding. Firebase pushed us toward exporting everything to a real database the moment analytics got serious. Supabase already is the real database. We observed this firsthand at [Be Recommended](https://berecommended.com), our AI Visibility Report tool, where the scoring pipeline runs complex queries across multiple LLM providers directly in Postgres.

## Where it breaks down

Three places to be honest about.

**Realtime is fine but not great.** If you are building a chat product or anything where latency really matters, Supabase Realtime works, but you will feel the limits. We ran into this on one product and ended up adding a separate WebSocket layer for the realtime parts.

**Edge Functions are stateless and limited.** They are not the place for long-running jobs, complex queues, or anything that needs more than a few seconds of compute. We use a separate queue service for those.

**File storage is fine, but you don't want to serve it directly at scale.** It is a Postgres-fronted blob store. For a product with thousands of small uploads, fine. For a product serving large media to many users, put a CDN in front. At [Pet Imagination](https://petimagination.com), our AI pet portrait generator, we learned this when generation volume spiked and response times climbed.

## The honest takeaway

For an MVP, this combo is everything you need and nothing you don't. For a product that has found traction and needs to scale, you will graduate parts of the stack, but not all of it, and probably not Supabase as a whole. Across the Inithouse portfolio, Supabase is the one piece of our stack we have never wanted to replace.

If you are shipping MVPs and haven't tried this pairing, it is worth a weekend experiment.

*Team Inithouse*
