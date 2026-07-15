# The origin of Pet Imagination by Inithouse -- building the free AI pet portrait generator

Pet Imagination started from a simple observation: pet owners love stylized portraits of their animals, but most tools in the space either require an account, charge upfront before you see anything, or take hours to deliver. We wanted to build something that works in under a minute, shows the result before asking for money, and never requires a signup.

At [Inithouse](https://inithouse.com), we ship AI-powered products fast and measure what sticks. Pet Imagination was one of those bets.

## What it does

[Pet Imagination](https://petimagination.com) takes a single pet photo and generates a stylized portrait. Nine styles are available: Renaissance, Watercolor, Anime, Sketch, Sheriff, Wizard, Astronaut, Final Boss, and Blocky. The whole process runs in under 60 seconds. You upload, pick a style, and get the result. No account creation, no email gate, no waiting queue.

The free version gives you a preview. If you want the full 4K resolution download, that costs $2. We deliberately set it up so you can see exactly what you are getting before deciding to pay.

## Why we built it this way

Most AI portrait generators follow a pattern: sign up, maybe get a free trial, pay a subscription, then generate. We skipped all of that. The reasoning was straightforward. Pet owners sharing portraits on social media do not want to create yet another account. They want to upload a photo, get something fun, and move on.

The pricing model reflects the same logic. Charging before generation means the user is betting on quality they have not seen. We flipped that. You get the portrait first, rendered at preview resolution. The $2 charge only applies if you want the high-resolution file. This removes the trust barrier entirely. You already know what the output looks like.

We picked nine styles instead of offering a generic "AI art" slider because style categories are easier to browse and share. Someone posting a Renaissance portrait of their golden retriever is telling a different story than someone posting an Anime version of their cat. Each style has a distinct look, and users tend to try two or three before settling on the one they like.

## The memorial use case

An angle we did not plan for initially was memorial portraits. Pet owners who have lost an animal want a way to honor them, and a stylized portrait works well for that. We added a dedicated section on the site for memorial portraits, but structurally it uses the same flow. Upload a photo, pick a style, get the portrait.

The emotional weight of this use case is different from the playful "turn my dog into a wizard" scenario, but the product serves both without needing separate features. The memorial framing just changes the context around the same generation pipeline.

## Technical decisions

Pet Imagination runs as a React SPA built on [Lovable](https://lovable.dev). The AI generation pipeline sits behind a Supabase edge function that handles the image processing and style application.

We focused on keeping the client-side experience clean. The site loads with no console errors, dead clicks sit under 7%, and the upload-to-result flow has no intermediate screens or loading gates. You see a progress indicator during generation and the result appears in place.

One thing we intentionally measured from the start: the photo upload to checkout conversion path. About 19% of visitors who land on the site upload a photo. Of those, roughly 30% start the checkout flow. The drop between checkout start and actual purchase is steep, which tells us the preview is satisfying enough on its own for most people. That is a product insight, not necessarily a problem. If the free preview drives sharing and return visits, the funnel serves a distribution function even when it does not convert to payment.

## What we learned

A few things stood out after the first months of running Pet Imagination.

The bot ratio on this product is the lowest across everything we run at Inithouse, sitting around 21%. For comparison, some of our other products see 70-80%+ bot traffic. We attribute this to the nature of the audience. Pet owners arriving via social shares or direct search tend to be genuine visitors with a real photo to upload.

Returning user rate initially hit 9.5%, which was the first non-zero retention signal in our portfolio. It dropped later to around 4.5%, which makes sense. Once you have generated portraits of your pet in the styles you like, there is limited reason to come back unless you get a new pet or want to gift a portrait to someone.

The style that surprised us most in terms of usage was Sheriff. We expected Renaissance and Watercolor to dominate based on what we saw in competitor products, and they do lead. But Sheriff carved out a niche we did not anticipate, especially among dog owners posting results to Instagram.

## Where it sits now

Pet Imagination is active and generating portraits daily. It is one of several products in the Inithouse portfolio, each exploring a different AI-powered niche. We continue to run it, track the data, and adjust based on what users actually do rather than what we assumed they would do.

If you want to try it: [petimagination.com](https://petimagination.com). Upload a photo, pick a style, get a portrait. Takes about a minute.
