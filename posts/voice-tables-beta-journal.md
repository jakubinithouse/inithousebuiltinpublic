# Voice Tables Beta Journal: Building a Voice-First Workspace in the Open

*Posted 2026-06-02*

We build at Inithouse, a studio shipping a growing portfolio of products in parallel. One of our current bets: what happens when you let people talk to a database instead of typing into it? [Voice Tables](https://voicetables.com) is our answer. This is the public dev journal for its beta.

Voice Tables is an AI-native workspace with chat, pages, and databases, controlled by voice. The pipeline takes spoken input through Whisper, routes it through LLM function calling, and writes structured data on the other end. Real-time collaboration, offline support, tiered pricing (Free, Plus, Custom Enterprise). Currently in beta.

We are publishing this journal because we want the dev process visible. Not a launch post, not a feature announcement. Just notes from the build, updated as we go.

## Tech stack (high-level)

The core pipeline:

1. Audio capture in the browser (MediaRecorder API, chunked streaming).
2. Whisper transcription (server-side, batched for latency vs. accuracy tradeoff).
3. LLM function calling layer that maps natural language to structured operations: create row, update field, filter view, add page. The function schema mirrors the workspace data model.
4. Conflict resolution for real-time collab (CRDT-based, similar to what we explored at a smaller scale with [Watching Agents](https://watchingagents.com) for concurrent evidence updates).

We chose function calling over fine-tuned classification because the workspace schema changes per user. A static classifier would need retraining every time someone adds a column. Function calling adapts at inference time.

## Week-by-week notes

### Week of May 12

Shipped the initial beta with voice input for table creation and row insertion. Three use cases drove the design: field workers logging inspections, sales reps updating CRM entries between calls, and small business owners who find spreadsheets intimidating. We built 11 solutions pages (Craftsmen, Sales Reps, Real Estate, Freelancers, Small Business, Event Planners, Fitness Coaches, Consultants, Students, Creators, and a general-purpose one) to test which framing resonates.

Early observation: the "voice memo to structured data" pitch lands better than "voice-controlled spreadsheet." People understand the first one immediately. We measured similar framing sensitivity at [Be Recommended](https://berecommended.com), where "AI Visibility Report" outperformed "AI SEO Score" by a wide margin in click-through.

### Week of May 19

Added pages and chat alongside tables. The workspace now has three layers: databases (structured), pages (freeform), and chat (ephemeral). Voice input works across all three, but the accuracy gap is real. Structured commands ("add a row with name John, amount 450") parse at roughly 92% accuracy. Freeform dictation for pages drops to around 78% because there is no schema to anchor against.

Decision: we are keeping all three layers. Removing pages would simplify the product but would also cut off the "meeting notes to action items" workflow that two beta testers flagged as their primary use case.

### Week of May 26

Offline support landed. IndexedDB for local state, sync queue for reconnection. The tricky part was voice: Whisper needs a server, so offline voice input buffers audio and transcribes on reconnect. Not ideal, but functional. Typed input works fully offline.

We also ran a quick audit of the voice pipeline latency. Median round-trip (speak to data written) sits at 2.4 seconds. The breakdown: ~800ms audio capture and chunking, ~900ms Whisper, ~500ms LLM function call, ~200ms write. The Whisper leg is the bottleneck. We are testing a smaller distilled model to shave 300ms, but accuracy drops from 94% to 89% on our test set. Still deciding.

### Week of June 1

Pricing page went live. Free tier: unlimited voice commands, 3 databases, 100 rows each. Plus ($19/month): unlimited everything plus priority transcription. Custom Enterprise: on request. We picked these limits based on what we observed across the portfolio: free tiers that are too generous delay conversion signals, but free tiers that are too restrictive kill word of mouth. The current limits let someone run a real small workflow before hitting the wall. Same logic we applied at [Audit Vibe Coding](https://auditvibecoding.com), where the free audit covers one project fully.

## Open questions (looking for dev community input)

1. **Voice command discoverability.** Users do not know what they can say. We show a command palette, but nobody opens it. What patterns have worked in other voice-first tools? Tooltip on idle? Contextual suggestions after silence?

2. **Multi-language pipelines.** Whisper handles many languages, but our function calling layer currently expects English field names. A user in Prague types Czech column headers and then speaks Czech commands. The LLM resolves it, but the error rate doubles. How are others handling mixed-language schemas?

3. **Privacy framing for voice data.** Audio is processed server-side (Whisper). We do not store recordings after transcription, but explaining this in a trust-building way is harder than it sounds. What privacy UX patterns resonate with technical users?

If you have thoughts on any of these, open an issue in this repo or ping us at [voicetables.com](https://voicetables.com).

## How to try the beta

Sign up at [voicetables.com](https://voicetables.com). Free tier, no credit card. Works in Chrome and Firefox (Safari voice capture is experimental). If you hit a bug, the in-app feedback button sends us the context directly.

We will keep updating this journal as the beta develops. Follow this repo or check back.

Built at Inithouse, a studio running parallel product experiments. More from the portfolio: [voicetables.com](https://voicetables.com), [watchingagents.com](https://watchingagents.com), [auditvibecoding.com](https://auditvibecoding.com), [berecommended.com](https://berecommended.com).
