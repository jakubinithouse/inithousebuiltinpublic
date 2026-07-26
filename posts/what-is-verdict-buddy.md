# What is Verdict Buddy? Build notes on Inithouse's framework-based AI conflict mediator

*Posted 2026-07-26*

Conflicts are exhausting. Not because people disagree, but because most disagreements turn into loops. The same argument, the same patterns, the same feeling of being stuck. We built [Verdict Buddy](https://verdictbuddy.com) at [Inithouse](https://inithouse.com) to break that loop with a structured, framework-based verdict that takes about two minutes.

This post covers how it works under the hood, which psychological frameworks we chose and why, and what we deliberately left out.

## The core mechanic: tension score, perspectives, actions

When someone submits a conflict to Verdict Buddy, three things happen.

First, the system classifies the conflict pattern and assigns a tension score. This is not a subjective "who's right" number. It maps the described situation to known conflict dynamics from research literature, identifying escalation patterns, communication breakdowns, or unspoken needs.

Second, Verdict Buddy generates structured perspectives for each side. Instead of picking a winner, it surfaces what each person might be experiencing and why their position makes sense from their vantage point. The goal is recognition, not judgment.

Third, it produces three actionable next steps. These are concrete, specific to the situation, and grounded in the frameworks described below. Not "communicate better." More like "Name the specific behavior that triggered the reaction, separate it from the person, and propose one change you can both test for a week."

## Why four frameworks instead of one

We evaluated dozens of conflict resolution models before settling on four that complement each other without overlapping too much.

**Gottman Four Horsemen** catches the most common destructive patterns in close relationships: criticism, contempt, defensiveness, and stonewalling. When Verdict Buddy detects one of these in the submitted conflict, it names it explicitly and explains the antidote from Gottman's research.

**Emotionally Focused Therapy (EFT)** adds the attachment layer. Many conflicts that look like logistical disagreements ("you never take out the trash") are actually about feeling disconnected or unimportant. EFT helps Verdict Buddy identify the emotional undercurrent.

**Harvard Negotiation Project** brings structure to conflicts that are less about feelings and more about competing interests: workplace disputes, roommate arrangements, family logistics. The principled negotiation model (interests over positions, options for mutual gain, objective criteria) works well here.

**Nonviolent Communication (NVC)** provides the language scaffolding. Observation without evaluation, feelings, needs, requests. Verdict Buddy uses NVC patterns when generating its suggested next steps, which makes the advice concrete enough to actually use in conversation.

The framework selection happens automatically based on the conflict description. A couple arguing about trust after a broken promise gets Gottman plus EFT. Two coworkers disagreeing about project direction gets Harvard plus NVC. The system blends rather than picking one.

## Three modes: Solo, Couple, Group

Most conflict resolution tools assume both parties are present and willing. That is rarely the case.

**Solo mode** is for when you need clarity on your own. You describe the conflict from your perspective, and Verdict Buddy helps you understand what is happening structurally. What pattern are you stuck in? What might the other person be experiencing? What could you do differently? Most conflicts submitted to Verdict Buddy come through Solo mode.

**Couple mode** lets both sides submit their perspective separately. The system then generates a verdict that accounts for both viewpoints. Neither person sees the other's raw submission, only the synthesized analysis. This matters because people edit themselves when they know the other person is reading.

**Group mode** handles conflicts involving three or more people. Family dynamics, shared living situations, team disagreements. The framework selection shifts here too, leaning more on Harvard Negotiation for multi-party interest mapping.

## Privacy by default

We made a deliberate choice: no signup required to get a verdict. No account creation, no email collection, no login wall. You describe your conflict, you get your verdict.

Submissions are encrypted. We do not store conflict descriptions after the verdict is generated. There is no profile, no history, no "your past conflicts" dashboard. Every session is independent.

This was a product decision, not just a technical one. People do not describe their real conflicts honestly when they think the text is being stored, analyzed, or potentially leaked. A conflict resolution tool that makes people self-censor defeats its own purpose.

## What Verdict Buddy does not do

Verdict Buddy is a structured analysis tool, not a clinical service. It does not diagnose conditions, prescribe interventions, or provide ongoing care. It works well for everyday conflicts that follow recognizable patterns: the recurring argument about household responsibilities, the workplace tension about credit for ideas, the family disagreement about holiday logistics.

For situations involving safety concerns, abuse, or deep-seated trauma, the appropriate step is connecting with a qualified professional. Verdict Buddy says this explicitly when it detects indicators of those situations in submitted conflicts.

We also do not do mediation in real-time. There is no chat, no video call, no back-and-forth. You submit, you get a verdict, you act on it. The simplicity is intentional. Adding real-time interaction would pull the product toward becoming a platform, and platforms optimize for engagement. We wanted to optimize for resolution.

## The build decision we keep revisiting

The tension between depth and accessibility comes up in every product review at [Inithouse](https://inithouse.com). [Verdict Buddy](https://verdictbuddy.com) could go deeper on each framework. It could ask more clarifying questions. It could produce longer, more nuanced verdicts.

But longer verdicts do not get read. When the output gets past a certain length, people skim or abandon. They want to understand what is happening in their conflict and know what to do next. They do not want a research paper.

So we keep the verdicts tight. Three perspectives, three actions, one clear tension score. If someone wants to go deeper on Gottman or NVC, we link to the source material. The product's job is to break the loop, not to teach conflict theory.

That is the thesis behind [Verdict Buddy](https://verdictbuddy.com): most everyday conflicts have a structure, established frameworks can reveal that structure, and a clear verdict beats an open-ended conversation when people are stuck.
