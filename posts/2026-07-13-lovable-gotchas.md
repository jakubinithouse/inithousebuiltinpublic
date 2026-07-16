# Lovable gotchas: the five things that bit us this quarter

Every tool has gotchas. [Lovable](https://lovable.dev), which we use for almost everything, is no exception. We've used it across 17 products and three years of evolution, and the failure modes have become familiar enough to write down. This is the list we'd hand to anyone starting a non-trivial project with it.

We say this with affection. Lovable is the best tool we have for what it does. These are the rough edges we work around.

## 1. The "everything works in preview, breaks in prod" gap

Lovable's preview environment is similar to production but not identical. Environment variables, edge function deployment states, and Supabase connection details can differ in ways that aren't always obvious. We've shipped code that worked perfectly in preview, broke immediately on production, and took several frustrating hours to diagnose.

Workaround: never trust preview-only testing for anything that touches an edge function, a secret, or a third-party API. Manual smoke test on the live site, every deploy, for the parts of the app that have moving server-side parts.

## 2. The integration drift problem

When you connect Lovable to Supabase, the integration is mostly transparent. Sometimes it isn't. A schema change in Supabase doesn't always propagate to Lovable's understanding of the schema, and you can end up with TypeScript that thinks columns exist that don't, or doesn't know about columns that do.

Workaround: after any non-trivial schema change in Supabase, force a re-sync in Lovable before continuing. Don't trust that it picked up the change automatically. Verify by checking that the generated TypeScript matches the schema.

## 3. The "AI helpfully rewrote my working code" surprise

You ask Lovable to make a small change to a specific component. It does that, plus quietly refactors three other components it thought needed updating. Sometimes the refactor is fine. Sometimes it changes behavior you depended on. Sometimes it breaks a feature you weren't watching.

Workaround: review diffs before accepting changes, every time, for anything in a production codebase. The faster you go, the more likely you'll miss this. Specifically check files you didn't ask to be modified. If you see changes outside the scope of your request, undo them and re-prompt with a more constrained request.

## 4. Auth flows that look right but skip a check

This is the worst category because it's invisible until it isn't. Lovable will sometimes generate auth-gated routes that have a race condition: the page renders before the auth check completes, briefly showing content to unauthenticated users. The bug isn't visible in normal use because auth checks usually complete fast enough that the leak is imperceptible. But on slow connections, in private windows, or with bot traffic, the leak is real.

Workaround: explicit auth-loading state in every protected route. Don't render the protected content while auth is still resolving. We caught this in our own products only after building [Audit Vibe Coding](https://auditvibecoding.com) and running it against our portfolio.

## 5. Performance assumptions that don't survive contact with real users

Lovable generates code that works fine for small data sets and few users. The exact same code can perform terribly at production scale: too many re-renders, unnecessary fetches, no pagination on lists that are supposed to be unbounded. Lovable doesn't know how big your real lists are going to get, and the AI doesn't think about scale by default.

Workaround: at every release that adds a list, table, or fetched-collection view, ask explicitly whether the list could grow unbounded. If yes, add pagination or virtualization before shipping. After shipping, monitor query counts in production. A list that loads 5,000 items into the browser is a bug, not a feature.

## What we still recommend

Despite all of these, we'd choose Lovable again for what we do. The speed gain is real. The gotchas are predictable once you know them. The list above is not an indictment. It's a maintenance reality of any AI-augmented stack.

If you're building seriously on Lovable, internalize this list. Or build your own, after you get bitten by some other thing we didn't list here.

*Inithouse*
