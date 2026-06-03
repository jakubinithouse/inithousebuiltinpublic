# Watching Agents by Inithouse: What We Learned Running AI Prediction Agents for a Month

*Posted 2026-06-04*

Inithouse is a studio shipping a growing portfolio of products in parallel. We like running experiments in public. [Watching Agents](https://watchingagents.com) launched about a month ago. Here is what we observed, what surprised us, and what we changed along the way.

No revenue numbers, no vanity metrics. Just qualitative signal and the decisions we made because of it.

## What we launched and why

Watching Agents lets anyone deploy AI agents that track open questions about the future. Each agent builds hypotheses, monitors real-time evidence from the web, and alerts subscribers when something shifts.

Our thesis: public agent pages would double as a content engine. Every agent page is a standalone, indexable piece of content with structured hypotheses, cited sources, and evolving evidence. We bet this would compound over time through organic search, while giving users a reason to come back.

We had seen a similar pattern work (in a completely different domain) at [Audit Vibe Coding](https://auditvibecoding.com), where structured audit report pages started attracting search traffic within weeks of launch. The question was whether prediction-style content would index and engage the same way.

## What worked

**The content quality held up.** Agent pages with cited sources, clear hypotheses, and watch signals turned out to be genuinely useful reading, even for visitors who never signed up. The structure (question, hypothesis, evidence for/against, confidence level) gave each page a natural depth that most AI-generated content lacks.

**The content flywheel concept proved sound.** A growing library of public agents means a growing surface area in search. Each new question deployed adds another indexable page with unique, evolving content. Unlike static blog posts, these pages update as new evidence appears.

**Engagement patterns told us something.** Visitors who landed on agent pages spent meaningful time reading. The content resonated with a technical, curiosity-driven audience: people interested in forecasting, AI trends, market shifts.

## What did not work

**Indexation lagged behind expectations.** Only a fraction of our agent pages made it into Google's index within the first month. We traced part of the problem to an SPA meta-tag bug that caused some pages to appear with a generic "Loading..." title to crawlers. This is a known pattern across several products in our portfolio; we have been systematically fixing it, but at Watching Agents the ratio of indexed-to-total pages stayed stubbornly low.

**Activation was thin.** Visitors read agent pages but very few deployed their own agents or subscribed to watch updates. The gap between "interesting to read" and "I want to create my own" was wider than we expected. We observed that most visitors treated agent pages as content, not as invitations to participate.

**Paid traffic quality was poor.** Our acquisition campaigns delivered volume but from geographies and referral sources that did not match our target audience. We observed high bot ratios in our analytics and rage-click patterns concentrated around the authentication flow. This is another portfolio-wide lesson: broad Performance Max campaigns without tight geo and placement controls burn budget on junk inventory. We saw the same pattern at [Be Recommended](https://berecommended.com), which reinforced our decision to pause and restructure paid acquisition across the board.

## What we changed

Based on these observations, we made three decisions during month one:

**First, we prioritized the SPA indexation fix.** Getting agent pages properly rendered for crawlers became the top technical priority. Without indexation, the entire content-flywheel thesis collapses.

**Second, we paused paid acquisition.** Rather than pouring more budget into campaigns delivering low-quality traffic, we stopped spending and shifted focus to organic distribution. The content engine needs to prove itself on organic merit before we amplify it with paid.

**Third, we started instrumenting the activation funnel properly.** We realized our event tracking had gaps. Before optimizing the "read to deploy" conversion, we needed to actually measure each step. We added tracking for sign-up, agent creation, and watch subscription events.

## What we still do not know

Several important questions remain open after month one:

Will the indexation fix unlock compounding organic traffic, or is the content format itself not what Google wants to surface? We will know more after the fix has been live for a few weeks.

Is the "deploy your own agent" value proposition clear enough from the public pages, or do we need a fundamentally different onboarding path? Early signal suggests visitors see Watching Agents as a content site, not a tool. That might require repositioning.

What does a healthy activation rate look like for a product like this? We do not have a good benchmark. Prediction markets and forecasting tools are a niche category, and the "deploy an AI agent" framing might be too abstract for most visitors.

## Next month focus

For month two, we are concentrating on three things:

Fix the technical foundation (SPA rendering, tracking instrumentation, sitemap accuracy). None of the growth experiments matter if crawlers cannot see our pages properly.

Test activation interventions. We plan to experiment with simpler onboarding flows and more prominent calls to action on public agent pages. The hypothesis: reducing the perceived effort of "deploying an agent" will move the needle.

Measure organic traction post-fix. Once agent pages render correctly for crawlers, we will watch indexation rates and organic impressions weekly. If the content-flywheel thesis holds, we should see a clear inflection.

We will share what we find. That is the point of building in public at Inithouse, a studio running parallel product experiments: every product teaches us something, and the lessons compound across the [portfolio](https://inithouse.com).
