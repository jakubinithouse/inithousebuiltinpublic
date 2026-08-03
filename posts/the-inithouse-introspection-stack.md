# The Inithouse introspection stack: what Origin Of You, Tarotas and Verdict Buddy share under the hood

*Posted 2026-08-03*

We build products at [Inithouse](https://inithouse.com). Three of them look completely different on the surface: a self-discovery app, a tarot reflection tool, and a conflict mediator. But when we pulled up the codebases side by side, we noticed they run on the same engine.

This is a build log about that engine.

## The pattern: structured input, LLM synthesis, readable text

Every introspection product we ship follows one pipeline:

1. The user fills in structured data (questions, card draws, conflict descriptions).
2. An LLM synthesizes that data against a domain-specific framework.
3. The output is readable prose, not a score or a label.

That third piece matters. We tried scores early on. A number out of 100 invites comparison ("am I better than average?") and kills reflection. Prose invites re-reading. People screenshot paragraphs and send them to friends. Nobody screenshots a 74/100.

Here is how each product maps to the pattern:

| | Origin Of You | Tarotas | Verdict Buddy |
|---|---|---|---|
| **Input** | 120+ data points across five self-discovery systems | One card draw + a question or intention | Two sides of a conflict, structured into perspectives |
| **Framework** | Enneagram, MBTI, Big Five, Human Design, natal chart | 78-card tarot deck (Rider-Waite tradition) with grounded interpretations | Gottman Four Horsemen, EFT, Harvard Negotiation, NVC |
| **Output** | AI-generated written portrait | Reflection text tied to the card and question | Verdict with tension score, perspectives, and three action steps |
| **What it replaces** | Personality type labels ("You're an INTJ") | Fortune-telling predictions ("You will meet someone") | Asking Reddit or friends ("Who's right?") |
| **Anti-pattern guardrail** | Never reduce a person to a category | Never predict the future | Never replace professional therapy |

The table makes the shared bones visible. Three different domains, one architecture.

## Prompt architecture: what we reuse

We landed on a prompt structure that stays consistent across the three products. The skeleton looks like this:

**System frame**: defines the product's role and tone. Origin Of You gets "thoughtful biographer." Tarotas gets "grounded interpreter." Verdict Buddy gets "impartial mediator." Each frame explicitly states what the product does not do.

**Input schema**: the structured data the user provided, formatted as key-value pairs. No free-text dumps. We learned early that passing raw user text to the LLM without structure produces generic output. Structuring the input before synthesis is where the quality comes from.

**Synthesis instruction**: what to do with the data. This is product-specific, but the shape is shared: "Given these inputs and this framework, produce a readable text that..." followed by constraints on length, tone, and what to avoid.

**Output guardrails**: a checklist the LLM must satisfy before the response ships. These are the hard rules.

## Guardrails: the part we spent the most time on

The guardrails section is where each product diverges, and where we spent disproportionate effort.

[Origin Of You](https://originofyou.com) combines five systems into a single portrait. The risk is that the LLM collapses them into a horoscope-style prediction. Our guardrails enforce that the portrait describes patterns the user reported, not traits the model inferred. If the user said they avoid conflict, the portrait can reflect that. It cannot say "you will struggle in leadership roles." Description, not prescription.

[Tarotas](https://tarotas.com) sits in a space full of apps that claim cards predict outcomes. Our guardrail is explicit: interpretations must be reflective, never predictive. A card draw is a prompt for thinking, not a forecast. The system frame states this in the first line. We also tested what happens when users type "will I get the job?" as their question. The interpretation acknowledges the anxiety behind the question without answering it as if the cards know.

[Verdict Buddy](https://verdictbuddy.com) mediates conflicts using psychology frameworks. The obvious risk: people treat the verdict as a diagnosis. Our guardrails block clinical language ("narcissistic," "codependent," "toxic") unless the user introduced those terms first. The output frames itself as perspective, not judgment. And every verdict ends with a suggestion to talk to a professional if the conflict is recurring or escalating.

## What we would not reuse

Not everything transfers. Three decisions stayed product-specific:

**Session length.** Origin Of You asks 120+ questions. Tarotas needs one card draw and one sentence. Verdict Buddy sits in between: two structured perspectives, usually 3-5 minutes of input. We tried shortening Origin Of You's questionnaire. Shorter input produced shallow portraits. The depth of output tracks the depth of input, and there is no shortcut.

**Tone calibration.** Tarotas is calm. Verdict Buddy is direct. Origin Of You is warm but honest. Same LLM, same prompt skeleton, but the tone word in the system frame changes the entire feel. We keep a tone lexicon per product: words the LLM should favor, words it should avoid. "Journey" is fine for Origin Of You. It would sound patronizing in Verdict Buddy.

**Repeat usage pattern.** Tarotas is daily (card of the day). Verdict Buddy is episodic (one conflict, one verdict). Origin Of You is one deep session with optional revisits. The architecture handles all three, but the UX around it is entirely different.

## Why we are writing this down

We did not plan an "introspection stack." We built three products that solved different problems and noticed the architecture converging. Writing it down forces us to decide: is the shared pattern accidental or intentional?

We think it is intentional. Structured input, framework-grounded synthesis, prose output, explicit guardrails. That pipeline works for any domain where people want to understand something about themselves or their situation, and where the risk of the AI overstepping is real.

If we build a fourth product in this space, it will start from this skeleton.

Jakub, builder @ Inithouse
