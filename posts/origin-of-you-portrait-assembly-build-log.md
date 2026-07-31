# Five systems, 120+ data points, one written portrait: how Origin Of You assembles its output

*Posted 2026-07-31*

[Origin Of You](https://originofyou.com) is a self-discovery app that combines five personality and behavioral systems into a single AI-generated written portrait. The input: over 120 data points collected across MBTI, Big Five, Enneagram, Human Design, and natal chart astrology. The output: a continuous text, roughly 800 to 1,200 words, that describes how your specific combination of traits, motivations, and patterns interact. This build log covers how we get from raw framework results to that final text.

## Why five systems and not one

Each framework captures a different layer of how a person operates. MBTI maps cognitive function preferences. Big Five measures personality on continuous scales. Enneagram targets core motivations and stress patterns. Human Design describes energy mechanics and decision-making authority. Astrology adds an archetypal dimension the other four ignore entirely.

The problem with using any single framework is that it leaves blind spots. MBTI says nothing about emotional regulation. Big Five has no model for motivation. Enneagram is categorical where Big Five is continuous. Stacking five systems does not eliminate blind spots, but it reduces them, and it surfaces contradictions that turn out to be the most interesting part of a portrait.

## What each system contributes

| System | Data points | What it adds to the portrait |
|--------|-------------|------------------------------|
| MBTI | ~8 | Cognitive function stack, information processing style, decision-making axis (T/F) |
| Big Five (OCEAN) | 5 | Continuous personality dimensions: openness, conscientiousness, extraversion, agreeableness, emotional stability |
| Enneagram | 3-4 | Core motivation, wing influence, instinctual variant (self-preservation / social / sexual) |
| Human Design | ~40 | Energy type, inner authority, profile, defined and undefined centers across 9-center chart |
| Astrology (natal chart) | 30+ | Sun/moon/rising, planetary positions across 12 houses, aspect patterns |

The total lands between 120 and 140 depending on chart configuration. Human Design and astrology contribute the bulk of the raw count because their charts encode more structural information than questionnaire-based systems.

## The normalization problem

Raw outputs from five frameworks are incommensurable. A Big Five percentile and an Enneagram type number live in completely different spaces. You cannot average them, and feeding all 120+ values into a single prompt produces incoherent output.

We built a normalization layer that maps every framework onto twelve shared semantic dimensions: relational orientation, decision-making style, energy management, conflict response, creative expression, and seven others. Each framework contributes to a subset of these dimensions through mapping functions we wrote by hand, not trained.

The conflict response dimension, for example, draws from Big Five agreeableness and neuroticism (weighted), Enneagram type (types 8, 9, and 1 map differently from each other and from the rest), MBTI's thinking/feeling axis, and Human Design authority type. The mappings are lookup tables with interpolation, built from cross-referencing the source literature of each framework against observed user patterns.

The result is a twelve-dimensional vector that captures where all five systems agree, where they diverge, and where the tensions sit. The tensions are what make portraits feel specific rather than generic.

## Resolving contradictory signals

Contradictions between systems are common. Someone scores high on Big Five extraversion but has a Projector type in Human Design, which operates on an invitation-based energy model. Someone tests as INTJ (internal, structured, analytical) but has an Enneagram 7 wing (novelty-seeking, scattered, experience-driven). These are not errors. They are the texture of a real person.

We handle contradictions explicitly rather than averaging them away. The normalization layer flags any dimension where two or more systems disagree by more than a threshold. These flagged tensions get surfaced in the synthesis step, and the portrait text addresses them directly. A typical line might describe how the person's analytical decision-making style coexists with an impulse to chase new experiences, and how that tension plays out in specific situations.

This is the main reason we chose a written portrait instead of a score or type label. A score flattens contradictions into a single number. A type label picks one system's framing and ignores the rest. A portrait can hold multiple truths at once and describe how they interact. That is closer to how actual humans work.

## Portrait generation: three stages, not one prompt

We do not send 120 data points into a single LLM call. The generation runs in three sequential stages.

Stage one produces a synthesis memo. The normalized twelve-dimension vector and the raw framework results go in. The model identifies the three to five most defining patterns and any flagged contradictions. Output: a structured memo of roughly 400 tokens. The user never sees this.

Stage two generates the portrait draft. The synthesis memo goes in as context alongside a style guide. The output is the actual portrait text in second person, organized around the patterns from stage one. No bullet points, no type labels in the text. The target is prose that reads like a letter written by someone who studied you, not a diagnostic report.

Stage three runs a consistency check. The draft goes back in with the original data for a verification pass. Does the portrait contradict any raw framework result? Does it make claims not supported by the input data? Does it default to generic language where specific patterns exist? Flagged sections get rewritten.

The three-stage approach costs more tokens than a single call but produces substantially better output. Single-prompt attempts tended to either ignore some systems entirely or list results framework by framework without integrating them.

## Why portrait instead of score

We considered and rejected several output formats before landing on prose. A radar chart is easy to scan but says nothing about how dimensions interact. A type label ("you are a Creative Connector") feels satisfying for about ten seconds and then becomes a box. A percentile breakdown is accurate but emotionally flat.

The portrait format works because self-discovery is a narrative activity. People want to see themselves described, not measured. The written format lets us say that a particular combination of high openness, anxious attachment triggers, and a 4w5 Enneagram profile creates a specific pattern in creative work, and then describe what that pattern looks like in practice. No chart does that.

The whole process takes about fifteen minutes of user input. No account required to start. The portrait stays private.

Try it at [originofyou.com](https://originofyou.com).
