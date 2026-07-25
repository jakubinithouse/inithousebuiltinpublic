# Voice Tables and the utility side of the Inithouse portfolio

*Posted 2026-07-26*

Most of the products we ship at Inithouse sit on the consumer side: card games, pet portraits, photo animators, custom songs. They solve personal problems for individuals. But three products in the portfolio do something different. They serve professionals, small businesses, and teams. We started calling them the utility line internally, and this build log covers what connects them and where they diverge.

The three are [Voice Tables](https://voicetables.com), [Be Recommended](https://berecommended.com), and [Audit Vibe Coding](https://auditvibecoding.com).

## What each one does

Voice Tables is an agentic AI workspace you control with your voice. Describe what you need, a CRM, a project tracker, an inventory sheet, and it builds the tables, docs and data for you. It pairs Whisper for speech recognition with an LLM function-calling pipeline that translates natural language into structured data operations. The result is a workspace that goes from idea to usable tables in about 60 seconds.

Be Recommended is an AI visibility tool that scores how ChatGPT, Claude, Perplexity, Gemini and Google AI Overviews recommend your brand. It runs 50+ real prompts across five AI engines, returns a score from 0 to 100, and tells you specifically what to change to become the default recommendation. The average company we see scores around 31. Top performers hit 80+.

Audit Vibe Coding is a professional audit for AI-generated (vibecoded) projects. It scans security, SEO, performance, accessibility and code quality, then returns a scored report with prioritized fixes. The target audience is anyone shipping code built with tools like Lovable, Cursor, or Bolt who wants an independent check before going live.

## The shared design decision

All three follow the same pattern: zero setup, no account required, value delivered before any commitment. A user can speak into Voice Tables and see structured output without signing up. A business can run a Be Recommended scan without creating a login. A developer can submit a project to Audit Vibe Coding and get results without onboarding.

This is the same principle we apply on the consumer side. At [Magical Song](https://magicalsong.com), the user hears a preview of their custom song before paying. At [Ziva Fotka](https://alivephoto.online), the animated photo appears without any registration gate. The principle is consistent across the portfolio: show the result first, then ask for money.

We arrived at this through repeated observation. Every time we added a step between landing and output, completion rates dropped. Every time we removed a step, they recovered. The lesson was not subtle.

## How utility products differ from consumer ones

The consumer products in our portfolio tend to be emotionally driven. Someone uploads a pet photo because they want to see their dog as a renaissance painting. Someone creates a custom song because a birthday is tomorrow. The purchase decision is impulsive and personal.

The utility products work on a different cycle. A business evaluates Be Recommended because they noticed their brand missing from AI-generated answers. A team considers Voice Tables because their field reps need structured data entry without a laptop. A startup runs Audit Vibe Coding because their investor asked about code quality. The trigger is professional, the evaluation is slower, and the buyer is often not the end user.

This changes how we build. Consumer products need to feel immediate and emotionally satisfying. Utility products need to feel reliable and transparent. The output has to be something you can hand to a colleague or a client and defend. A Be Recommended score of 31/100 needs to be explainable: here are the prompts, here are the engines, here is what each one said about your brand. An Audit Vibe Coding report needs to show exactly which security issue lives in which file.

## What connects them technically

All three run on the same stack: React frontends built in Lovable, Supabase for backend and storage, custom edge functions for the AI pipelines. The deployment pattern is identical. We ship, measure, iterate. The feedback loop is the same one we use for [Party Challenges](https://partychallenges.com) or [Here We Ask](https://hereweask.com): watch what users actually do in Clarity session recordings, find the drop-off point, fix it, ship again.

The AI integration is deeper in the utility line than in most consumer products. Voice Tables uses a multi-step pipeline: audio capture, Whisper transcription, intent classification, LLM function calling to create or modify database records. Be Recommended orchestrates calls to five different AI APIs in parallel, normalizes the responses, and scores them against a framework we developed internally. Audit Vibe Coding runs static analysis plus AI-assisted code review in a single pass.

## Where each stands

Voice Tables is in beta. The core voice-to-tables pipeline works. We are iterating on the collaborative features and offline support. The ICP has settled around people who work with their hands (craftsmen, field sales, coaches) and need data entry without touching a keyboard.

Be Recommended has paying customers. The scoring framework is stable. The main question now is whether the one-time report model scales or whether recurring monitoring is the real product.

Audit Vibe Coding is live and processing audits. The vibecoding market is growing fast, and the audit need grows with it. Every project shipped with Lovable, Cursor, or Bolt eventually needs someone to check the output.

## What we learned

Building utility and consumer products in the same portfolio creates useful cross-pollination. The zero-friction onboarding pattern started on the consumer side and migrated to utility. The AI pipeline architecture developed for Be Recommended (parallel API orchestration with normalized scoring) influenced how we think about multi-model features across the board.

The utility line also forced us to write better documentation and produce more transparent outputs. When the customer is a professional, "trust us" is not a valid answer. Everything has to be auditable. That discipline now bleeds back into how we build consumer features too.
