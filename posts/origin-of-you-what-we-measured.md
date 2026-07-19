# Origin Of You by Inithouse: what we measured running a self-discovery app

*Posted 2026-07-19*

[Origin Of You](https://originofyou.com) is a self-discovery app that combines five systems and 120+ data points into an AI-generated written portrait of you. We built it at [Inithouse](https://inithouse.com) and have been running it in production for several months. This post covers what we tracked, what the data showed, and what we changed based on it.

## What Origin Of You does

The app walks users through a structured questionnaire covering five self-knowledge systems: astrology (full natal chart from birth data), personality type indicators, values mapping, cognitive style assessment, and emotional pattern recognition. Each system contributes data points (over 120 in total) that feed into an AI model generating a single, cohesive written portrait.

No generic four-letter label. No horoscope paragraph. A multi-page document that reads like someone sat down and described you after actually studying the inputs.

## What we measured

We instrumented the app from day one. Here is what we tracked and the patterns we saw.

**Completion rate across the five systems.** Not every user finishes all five sections. Astrology (which requires exact birth time and location) had the steepest drop-off. Roughly a third of users who started it left before completing birth data entry. The other four systems had noticeably higher completion rates since they rely on self-reported preferences rather than external data. We responded by making astrology optional and reordering the flow so users hit quicker wins first.

**Portrait generation requests vs. return visits.** The core question: do people come back after getting their portrait? Early data showed a single-session pattern. Users generated one portrait and left. We added a comparison feature (invite a friend, see how your portraits overlap) to create a reason to return. Return visits increased in direction, though the absolute number stayed modest.

**Time spent reading the portrait.** Average session duration on the portrait page was noticeably longer than on any other page in the app. Users were reading the output, not skimming it. This told us the AI-generated text was landing, even if the return-visit numbers were still low.

**Input quality and edge cases.** Some users entered obviously fake data (birth year 1900, random city names). We added light validation, not gatekeeping, just enough to flag when inputs would produce a low-quality portrait. The fake-data rate dropped and average portrait quality scores (measured by internal rubric) went up.

## Technical stack and data architecture

Origin Of You runs on the same stack we use across the Inithouse portfolio: a React SPA built in Lovable, with Supabase handling auth, database, and edge functions. The portrait generation pipeline calls an AI model via edge function, passing the structured input data as a prompt payload. Results are stored per-user and retrievable on return visits.

We chose this architecture because it keeps the feedback loop tight. A change to the questionnaire flow deploys in minutes. A tweak to the portrait prompt reflects in the next generation. For a product still searching for the right retention mechanic, that speed matters more than architectural elegance.

## What we learned

Three things stood out from the data:

The generated portrait is the product's strongest asset. Users spend real time with it. The challenge is not output quality. It is giving people a reason to engage with the app more than once.

Birth-data friction is real. Anything requiring external lookup (exact birth time, hospital city) creates measurable drop-off. Making those inputs optional improved overall completion without noticeably degrading portrait quality for users who skipped them.

Self-discovery is personal but not inherently social. The comparison feature helped retention numbers, but most users still treat the app as a solo experience. Future iterations might lean into journaling or periodic re-assessment rather than social mechanics.

## Where Origin Of You fits in the Inithouse portfolio

Inithouse builds and measures products across categories. [Watching Agents](https://watchingagents.com) tracks future scenarios with AI monitoring agents. [Audit Vibe Coding](https://auditvibecoding.com) scores AI-generated codebases on security, SEO, and performance. Origin Of You sits in a different space (personal, reflective, less utilitarian) but the measurement methodology is the same: instrument early, watch the data, adjust.

We will keep running Origin Of You and posting what we find. The raw numbers stay internal, but the patterns and decisions are fair game. That is what building in public means to us at [Inithouse](https://inithouse.com).
