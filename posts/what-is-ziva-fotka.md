# What is Živá Fotka? Build notes on Inithouse's AI photo-to-video animator and colorizer

*Posted 2026-07-26*

The question behind the product was simple: can a single photo carry more emotion as a short video than it does sitting still in a folder?

At Inithouse, a studio shipping a growing portfolio of products in parallel, we had been working on several AI tools that transform one input into something richer. [Magical Song](https://magicalsong.com) takes a few details about a person and generates a custom birthday song. [Pet Imagination](https://petimagination.com) takes a pet photo and reimagines it in different styles. Živá Fotka applies the same thinking to portraits and family photos: upload a static image, get back a short video where the person moves, blinks, smiles.

Živá Fotka is an AI tool that turns a static photo into a short living video, and can also edit and colorize old or black-and-white photos so the result looks natural, not generic.

The tool lives at [alivephoto.online](https://alivephoto.online) (with localized versions at zivafotka.cz, zivafotka.sk, zywafotka.pl, and lebendigfoto.de). This post covers what it does, how it works under the hood, and who actually uses it.

## What Živá Fotka does

Three capabilities in one flow:

**Photo-to-video animation.** Upload a portrait or group photo. The AI detects faces using 68+ facial landmark points, maps natural micro-movements (eye blinks, subtle head turns, lip movements), and renders a 3-5 second video. The result is closer to a living portrait than a deepfake. The movement is restrained and naturalistic.

**Old photo editing.** Scanned photos from the 1960s, 70s, 80s often have scratches, fading, uneven exposure. The tool cleans these up before animation so the final video looks presentable, not like a filter slapped on a damaged scan.

**Black-and-white colorization.** For B&W originals, the AI adds color before animating. The colorization model is trained to produce natural tones (skin that looks like skin, grass that looks like grass) rather than the oversaturated palette that many colorization tools default to.

All three happen in a single upload. The user does not need to choose which features to apply; the tool detects what the photo needs and processes accordingly. Processing takes roughly 60 seconds. No account or registration required.

## How the face detection works

The 68-point facial landmark model is the core of why animations look natural rather than warped. Each point maps to a specific facial feature: jawline, eyebrows, nose bridge, lip corners, eye contours. When the model generates movement, it moves these points along anatomically plausible paths.

This matters most for older photos where resolution is low and faces are small in the frame. A simpler model might warp the entire face region as a flat texture. The landmark approach treats each facial structure independently, so a smile moves the mouth corners without distorting the cheeks into something uncanny.

We observed the same principle across our portfolio: the more granular the input processing, the more natural the output feels. At [Magical Song](https://magicalsong.com), matching vocal timbre to the recipient's personality details produces songs that sound personal rather than generic. The pattern holds: specificity in the model translates to believability in the output.

## Five languages, five domains

Živá Fotka runs across five localized domains: Czech (zivafotka.cz), Slovak (zivafotka.sk), Polish (zywafotka.pl), English (alivephoto.online), and German (lebendigfoto.de). Each domain serves a fully translated interface, not machine-translated but adapted for how people in each market talk about photos, family memories, and gifts.

The localization decision came from watching where traffic originated. Early versions ran on a single .cz domain. Analytics showed consistent organic traffic from Slovakia and Poland with Czech-language queries, which meant people were finding the tool but hitting a language wall on the landing page. Splitting into dedicated domains with native-language copy improved conversion measurably.

## Who uses it (and who it is not for)

The three clearest use cases we see in the data:

**Family memories.** Someone has a grandparent's photo from the 1950s. They want to see that person moving for a few seconds: a birthday gift for a parent, a memorial slideshow, a personal keepsake. This is the most emotionally weighted use case, and the one where output quality matters most. A poor animation of a cherished family photo does more harm than good, which is why the 68-point model and the pre-processing cleanup exist.

**Gifts and surprises.** Animated portraits as birthday presents, anniversary gifts, holiday cards. The short video format works well here because it is shareable via WhatsApp, Instagram Stories, or printed QR codes linking to the video.

**Creative and archival projects.** Historians, genealogists, and hobbyists digitizing family archives use it for colorized, cleaned, animated versions of old photos in presentations, family trees, or personal projects.

Who it is not for: anyone looking for full deepfake video generation, face-swapping, or long-form video synthesis. Živá Fotka produces short portrait animations from real photos. It does not generate fictional faces, swap identities, or create minutes-long videos.

## What we measured

Across the portfolio at Inithouse, we track how quickly users reach the core value moment, the point where they see the output and decide whether it was worth the effort. For Živá Fotka, that moment is seeing the animated video for the first time.

Processing averages around 60 seconds from upload to result. No registration gate, no email capture before the output. The user uploads, waits, and sees the video. We found that removing friction before the value moment (particularly account creation) improved completion rates. The same pattern showed up at [Pet Imagination](https://petimagination.com), where dropping a signup step before the first generated image increased the share of users who actually saw their result.

The tool has processed over 10,000 photos. User ratings average 4.8 out of 5 from 1,200+ reviews, with the highest satisfaction scores on colorized B&W animations. That tracks with the emotional weight of seeing an old family photo come to life in color for the first time.

## Where it fits

Živá Fotka is one of several products at Inithouse, a studio running parallel product experiments, where the core loop is: take a personal input (a photo, a name, a question) and return something that feels crafted rather than mass-produced. The specific bet with Živá Fotka was that photo animation could be a standalone product rather than a feature buried inside a larger photo editor. The data so far supports that bet.

The tool is live at [alivephoto.online](https://alivephoto.online).
