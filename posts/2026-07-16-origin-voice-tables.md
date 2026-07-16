# The origin of Voice Tables by Inithouse -- building the voice-first agentic AI workspace

Most workspace tools assume you already know their interface. You open the app, find the right menu, figure out the field types, and start entering data manually. We kept running into this pattern at [Inithouse](https://inithouse.com) when watching how people outside tech actually manage their work. A fitness coach tracking client sessions, a craftsman logging jobs and materials, a freelancer organizing invoices. They all have structured data needs, but the tools built for those needs assume a level of spreadsheet literacy that many do not have.

Voice Tables was our attempt to answer a specific question: what if the interface for creating a database was just talking?

## What it does

[Voice Tables](https://voicetables.com) is an agentic AI workspace controlled by voice. You describe what you need, and it builds the workspace for you. Say "I need a CRM for my roofing clients" and it generates the tables, columns, sample data, and a docs page. The whole thing appears in about 60 seconds. No templates to browse, no column types to configure.

The workspace has three components: tables (structured data), docs (freeform pages), and an AI chat that can query or modify everything. You can keep using voice for ongoing tasks, or switch to keyboard and mouse once the structure is in place. The system uses Whisper for speech transcription and an LLM function-calling pipeline to turn spoken intent into structured operations on tables and documents.

## Why voice

The voice-first approach came from watching a specific failure mode in other tools.

When someone who is not a spreadsheet person opens Notion or Airtable for the first time, they hit a wall almost immediately. What is a "relation" field? What does "rollup" mean? These are powerful concepts, but they require learning a data modeling vocabulary that many small-business operators and independent professionals never pick up. They end up using a fraction of the tool, or they abandon it and go back to paper notes and text messages.

Voice removes that barrier. You do not need to know what a relation field is. You say "link each client to their appointments" and the system figures out the data model. The person describes their business, not the schema.

We were also drawn to voice because of the audience we had in mind. Craftsmen working on a job site, fitness coaches between sessions, event planners walking through a venue. These are people whose hands are often occupied or who are moving between contexts. Typing into an app is a context switch. Speaking is not.

## How it works under the hood

The pipeline goes: microphone capture, Whisper transcription, LLM interpretation, function calls against the workspace state, UI update. Each voice command is translated into one or more structured operations. "Add a column for due date" becomes a schema modification. "Show me all clients who owe more than 500" becomes a filtered view query.

We built this on a Supabase backend with a React SPA on Lovable. Real-time collaboration uses Supabase subscriptions, so two people looking at the same workspace see changes as they happen. Offline support is handled through a local-first sync layer so the app remains usable without connectivity.

One design choice that shaped the product: we made every voice command reversible. If you say "delete the payments table" and realize that was wrong, you can undo it. This matters because voice input has a different error profile than typed input. People misspeak. The system mishears. The cost of a mistake needs to stay low, or people stop using voice entirely.

## What we are learning

Voice Tables is in beta, and we are still testing the core hypothesis. The product works. You can create a workspace by talking, add and query data, and get a functional setup in under a minute. Whether that translates into regular ongoing use is the open question we are measuring.

The initial creation experience seems to resonate. People land on the site, try the voice flow, and get a workspace. What happens after that first session is less clear. Do they come back to maintain and grow that workspace, or was the creation itself the interesting part? We are tracking this closely.

We built 11 solutions pages targeting specific audiences: craftsmen, sales reps, real estate agents, freelancers, small business owners, event planners, fitness coaches, consultants, students, researchers, and creators. The reasoning was that "voice-first workspace" is abstract, but "voice-first CRM for roofers" is concrete. Each solutions page frames Voice Tables through a specific use case with matching table structures and workflows.

## Where it fits

Voice Tables is one of several products we run at Inithouse, each testing a different AI-powered niche. Compared to something like our pet portrait generator or our conversation card game, Voice Tables sits at the more complex end of the spectrum. It is a productivity tool, not a single-use consumer product. The retention dynamics are completely different, and we are calibrating expectations accordingly.

The product is free to start with. A Plus tier at $19 per month adds higher usage limits and priority processing. We kept the free tier functional enough that someone can run a small workspace without paying. Conversion to paid is a signal that the workspace became important enough to invest in.

If you want to try it: [voicetables.com](https://voicetables.com). Describe your workspace, and it builds it.
