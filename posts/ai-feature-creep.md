# AI feature creep: when adding GPT makes your product worse

*Posted 2026-07-16*

Every product team has felt the gravitational pull: "could we add an AI feature here?" Sometimes the answer is yes and the product gets noticeably better. Sometimes the answer is yes and the product gets noticeably worse. The second case is more common than people admit, and the difference between them is worth thinking about carefully.

We run [Inithouse](https://inithouse.cz), a studio with 17 live products. We've made both mistakes. Here's what we've learned.

## What "AI features" do well

The clearest wins from AI features are in three places.

**Unstructured-to-structured.** Turning text, images, or audio into structured data. Take a free-form description and extract fields. Take an image and identify objects. Take a recording and produce a transcript. These features tend to be valuable, predictable, and easy to evaluate. Our product [Voice Tables](https://voicetables.com) started from this principle: speak your data, get a structured table back.

**Generation with a clear target.** Producing content of a specific shape: a song, a summary, an image, a formatted document. When the user knows what they're trying to make, AI generation is genuinely useful. [Magical Song](https://magicalsong.gift) works because the target is clear: turn a personal story into a song with real vocals.

**Categorization at scale.** Bulk-classifying things that would be tedious to classify manually: support tickets, expenses, leads, content. The accuracy doesn't have to be perfect, just better than the alternative of doing nothing.

These features are the ones we've seen actually improve products in our portfolio.

## What "AI features" do badly

**Chatbots bolted onto products that didn't need them.** This is the most common AI feature creep. A product has a clear interface; someone adds a chat box; users now have to figure out whether to use the UI or the chat for any given task. The chat is usually worse than the UI at the things the UI does, and the UI is worse than the chat at the things the chat does, and the user has to constantly choose. Net effect: worse product.

**Recommendations that pretend to be more than ranking.** "AI-powered recommendations" that turn out to be a normal sort algorithm with a label. The label is fine; the implied capability is misleading. Users notice when the recommendation isn't smarter than the simpler version they could have built themselves.

**Generation when the user didn't ask for it.** Auto-generating content as a "convenience" usually makes the convenience worse. The user has to read and reject the suggestion, which is more work than just doing the thing themselves.

**"AI" as marketing without substance.** A landing page that emphasizes the AI-ness of the product more than what the product does. This is a tell for a product team that has lost touch with their actual user.

## The question we now ask

Before adding any AI feature to any product, we ask: "If this feature works perfectly, what gets better for the user?"

If the answer is "it's the same as before, but faster": usually worth it.

If the answer is "we save the user from doing a thing they didn't mind doing": probably not worth it.

If the answer is "the product would be more impressive to investors": definitely not worth it.

If the answer is "we don't really know": definitely not worth it.

This question has killed at least a dozen proposed AI features in our portfolio in the last year. None of them have come back as ideas we regret killing.

## The harder question

The harder question is when to *remove* AI features that already shipped but aren't earning their keep. Removing features is unpopular. Someone uses every feature, even bad ones. But each feature has a maintenance cost, and AI features specifically have an ongoing model-cost and a brittleness cost (they break when the underlying model behavior changes).

We've removed three AI features from products in the last year. Each removal was preceded by data showing the feature was used less than expected and that users who used it didn't have better retention than users who didn't. The removals were fine. Nobody complained. The products got simpler.

If you have AI features that nobody's measuring, you should measure them. If you measure them and they're not earning their place, you should remove them. The pattern is the same as for any feature, except that AI features carry more emotional weight, which makes the removal feel harder than it should.

The product is the priority, not the AI. Always.

Inithouse
