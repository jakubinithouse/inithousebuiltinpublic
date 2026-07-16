# Spotlight: Audit Vibe Coding - auditing AI-generated codebases

*Posted 2026-07-11*

[Audit Vibe Coding](https://auditvibecoding.com) audits AI-generated codebases for the issues that AI-generated code tends to have. Security holes, dead branches, performance landmines, structural fragility: the specific failure modes that show up when most of the code was written by an LLM rather than a person.

The product exists because we ran into these issues in our own work, fixed them ad hoc, and realized the patterns were consistent enough to be detected systematically. If you ship products built with Lovable or any other AI code-generation tool, you've probably shipped some of these issues without knowing it.

## What "vibe-coded" actually means

The term started as a joke and stuck. "Vibe coding" describes the workflow where a developer doesn't write the code line-by-line. They describe what they want, accept what the AI produces, and iterate by description rather than by direct edit. The code works. The code ships. The code is sometimes a structural mess that the developer never read carefully.

We do this. Most studios using AI code tools do this. The question is what to do about the systemic risks it introduces.

## The patterns Audit Vibe Coding detects

A few examples of what it looks for:

**Unguarded API keys.** AI models will sometimes write code that hardcodes credentials. The developer accepts the code, the keys go into git, and the breach happens months later. We catch this and flag it.

**Auth bypasses in conditional branches.** A common LLM mistake: writing an auth check, then writing an "if loading: return" branch that runs *before* the auth check. The page renders, content briefly leaks, the auth check fires after the damage. Subtle in code review. Easy for our scanner to flag.

**SQL builder concatenation.** Even when the LLM is supposed to use parameterized queries, it sometimes produces string-concatenated SQL in less-traveled code paths. SQL injection in 2026, in supposedly modern code.

**Dead branches with active side effects.** AI-generated code accumulates conditional branches over iterations. Sometimes those branches are unreachable from the UI but still execute when called via API. Old endpoints that no longer have UI but still mutate data are a real vulnerability surface.

**Re-renders that fetch.** A specific React + Supabase pattern: a useEffect that fires fetches on every state change, including changes the user can trigger rapidly. AI-generated code is unusually prone to this. The site looks fine in dev; the database bills look terrible in production.

## How we use it ourselves

Audit Vibe Coding runs against every Inithouse product on a monthly schedule. Findings go into a triage queue. Most findings get a same-week fix. Some findings, like performance issues that aren't actually impacting users, get triaged down and revisited quarterly.

This is the kind of process we'd never have stood up manually. Reading every codebase carefully every month isn't viable at our scale. A scanner that produces a focused list of real issues is.

## What we'd say to anyone shipping AI-generated code

Be honest with yourself about what you've shipped. The code probably works. It probably also has issues you'd find embarrassing if a real audit caught them. Catching them yourself, with tools designed for this specific failure mode, is much better than the alternative of having them caught by a user, an attacker, or a billing surprise.

Audit Vibe Coding is one option. There are others. The important thing is to actually do the audit, not to assume the AI got it right.

The whole point of using AI to write code is to ship faster. Some of the time saved should go into checking that what you shipped doesn't have foot-guns waiting for you. We've calibrated, in our own work, that about 10% of the time saved on writing code with AI gets spent on auditing it. That ratio feels about right. Less than that, and the bugs accumulate. More than that, and you've defeated the point of using AI in the first place.

[Try it](https://auditvibecoding.com) on a project you've built with Lovable or similar. The first scan is free. You'll probably find at least one thing worth fixing.

\- Inithouse
