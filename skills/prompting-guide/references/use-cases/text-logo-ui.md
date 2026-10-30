# Text, logos, posters, thumbnails, UI and screens

Markers: **[tested]** = generated and reviewed in a source test reel. **[untested]** = not run in a source test. Unmarked = the source gave no status.

## Triggers

"text on the image", "headline on the poster", "make a logo", "my logo on the sign", "poster", "thumbnail", "YouTube thumbnail", "Shorts / Reels cover", "title card", "price / offer on the ad", "app screen in the video", "show the UI", "the text is gibberish", "the logo is misspelled", "game icon".

## Load these

| Need | File |
|---|---|
| Where text can sit per aspect (safe zones) | this file, step 6 |
| Product with copy on it | [product.md](product.md) ad pack and hero banner templates |
| Neon without fake letters, cars without badges | [../styles/film-stocks.md](../styles/film-stocks.md), [../styles/atmosphere.md](../styles/atmosphere.md) |
| Face on a thumbnail | [avatar-portrait.md](avatar-portrait.md) face-lock line |
| Game icons and title logos | [stylized-anime-pixel.md](stylized-anime-pixel.md) |
| UI in an ad | [ads-promo.md](ads-promo.md) |

Router shot types ([../model-router.md](../model-router.md)): `text-graphic`, `vector-flat`, `hero-still`, `product-still`.

Model notes (from the source skills): text in the image by default → GPT Image 2; very text-heavy premium → GPT Image 2.5 Flare ([../models/gpt-image.md](../models/gpt-image.md)); good text in cheap drafts → Ideogram V3 ([../models/ideogram.md](../models/ideogram.md)); icons and vector → Recraft V3 ([../models/recraft.md](../models/recraft.md)); photoreal face match with little or no text → Nano Banana Pro, which also renders quoted text in stills [tested] ([../models/nano-banana.md](../models/nano-banana.md)).

## Rule zero: video models garble UI and small text

- In any video shot, screens are `an even cool white glow`. Real UI goes in during the edit [tested].
- Everything else in a video or photoreal still: `No readable text, signs or logos` (stills: `No text, no logos, no watermark.`; video: `No text, no subtitles, no watermark.`).
- Paperwork closed or face down. Neon as bare tubes bent into loops and lines, "no letters or symbols anywhere". Cars: "no badges and no license plate".
- Do not generate fake product-app chrome (sidebars, nav, settings rows). Product beats are designed motion graphics built in the edit. No real app UI screenshots unless asked.

## Recipe: text in a still

1. **Pick a text-strong model** (above). Keep copy under 8 words. Thumbnails: 1 to 4 words.
2. **Quote the exact string** and say it once: `Headline text reading exactly "<TEXT>"`. For logos and brand names, quote it and spell it letter by letter.
3. **Name the type and placement**: `in a massive heavy sans-serif, <colour> with a thick black outline, placed <top left / top / left side>, never covering the face`.
4. **Close the door on extra text**: `No other text, no watermark.`
5. **Leave a clean zone** if text is added later: `the top third above the head is a plain uncluttered {wall colour} wall` [tested pattern].
6. **Check at the size people see it** (below).

### Logos

- A logo must say what the business is. A generic bird was rejected; a tattoo-shop badge (bird on crossed tattoo machines + a "TATTOO" ribbon) passed.
- Generate the logo first (text quoted and spelled letter by letter), check spelling, then pass it as a reference for any world shot that shows it on a sign: `the logo from image N, exact shapes, colors and letters, placed away from the face`.
- For the final lockup in the edit, use the vector logo file. A scaled-up PNG reads pixelated.
- No real platform, network or brand logos except the user's own.

### Thumbnail prompt (build in this order)

1. Reference manifest (with references only): `IMAGE REFERENCES: image 1 = CHARACTER 1 face; image 2 = brand logo.`
2. Frame: `Bold, high-impact YouTube thumbnail, <ratio>, one continuous scene, poster-grade, bright and punchy, not a muted film still.` For 9:16 add `faces and text in the upper two-thirds`.
3. Scene: the concept, concrete, true to the video.
4. Subject: `large in the foreground, chest-up, filling about half the frame, face crisply sharp.` Per referenced person: `CHARACTER 1 is the exact person from image 1: same face shape, eyes, nose, lips, jawline, skin tone, hairline and hair. Do not beautify or restyle the face. Expression: <physical description of one emotion>.`
5. Key element: only the one prop or effect that makes the gap.
6. Logo (if any): `the logo from image N, exact shapes, colors and letters, placed away from the face.`
7. Text: `Bold headline text reading exactly "<TEXT>" in a massive heavy sans-serif, <colour> with a thick black outline, placed <top left / top / left side>, never covering the face, nothing in the bottom-right corner. No other text, no watermark.` No text wanted: `No text, no letters, no watermark.`
8. Light and grade: `strong key light on the face, soft fill, bright rim light separating the subject from the background, vivid saturated colors, deep blacks, crisp highlights, background simplified with soft vignette.`

Make three variants that differ in exactly one line (expression, camera distance, or text color).

Thumbnail truth rule: exaggerate, never misrepresent. No invented results, people, quotes, numbers or products. Emotions are written physically: "eyebrows raised high, mouth open in a gasp, eyes wide". Text adds what the image cannot say; it does not repeat the title. One text color plus a thick outline or shadow.

### Edit pass (one change at a time)

```
Edit image 1. Change ONLY <the text to read exactly "NEW TEXT" | the expression to <emotion> | the background to <new background> | the rim light colour to <colour>>. Keep everything else exactly the same: face, identity, pose, clothing, logo, composition, lighting, colors.
```
Use a text-strong model when the edit is text.

### Icons

```
ONE isolated <coin | heart | key | sword> game icon, centered, fills 80% of a square canvas, thick dark outline, <STYLE BLOCK>, readable at 32 px, solid flat magenta #FF00FF background, no text, no shadow.
```
Buttons and HUD bars: draw them in code. The art is only the icon.

## Step 6: framing and safe zones by aspect

| Aspect | Subject | Clean space for text | Safe zones |
|---|---|---|---|
| 9:16 | eyes at ~37-40% of height, centred | top third above the head; lower third under the chest | keep text out of the top ~12% and bottom ~20% (app chrome) |
| 4:5 | eyes at ~40%, centred | top quarter | 6% margins (thumbnail source: 10%) |
| 4:3 | rule of thirds, horizon on a third | the sky band or the empty side | 5% margins |
| 16:9 | off-centre on a third | the empty half | 5% margins; captions in the lower third; thumbnails: nothing in the bottom-right (duration badge) |
| 2.39:1 letterbox inside any frame | middle 55% of the height | in the bars | faces never under a bar |

Paid 9:16 ads: keep the top 14% and bottom 20% free of product and text.
Write the framing into the prompt: "vertical frame, subject in the upper third, the sky band above clear for words".

## Legibility check

Downscale each image to 320 px wide (9:16: 320 px tall) and look. Text reads and is spelled exactly; face and emotion read at once; one focal point; nothing important in the covered corner. On-screen copy uses proper grammar and capitalisation (not all-lowercase) and no unverified numbers.

### Filled example (thumbnail, 16:9, no references)

```
Bold, high-impact YouTube thumbnail, 16:9, one continuous scene, poster-grade, bright and punchy, not a muted film still. A home kitchen counter with a sourdough loaf that has risen so high it pushes the oven door open. A man in his thirties with curly red hair and a flour-dusted navy apron, large in the foreground on the right, chest-up, filling about half the frame, face crisply sharp. Expression: eyebrows raised high, mouth open in a gasp, eyes wide. Bold headline text reading exactly "TOO MUCH YEAST?" in a massive heavy sans-serif, yellow with a thick black outline, placed top left, never covering the face, nothing in the bottom-right corner. No other text, no watermark. Strong key light on the face, soft fill, bright rim light separating the subject from the background, vivid saturated colors, deep blacks, crisp highlights, background simplified with soft vignette.
```

## Pitfalls → fixes

| Pitfall | Fix |
|---|---|
| Text garbled or misspelled | Quote the string again, fewer words, move the take to a text-strong model |
| Text too small | Fewer words, "large bold headline" / "massive heavy sans-serif" |
| Extra random text appears | "No other text, no watermark." |
| Logo letters wrong | Spell it letter by letter; generate the logo alone first, then pass it as a reference |
| Generic logo | The mark must show what the business does (object of the trade + a word ribbon) |
| UI on a screen in video is gibberish | "an even cool white glow"; real UI in the edit [tested] |
| Neon signs grow fake letters | Bare tubes, "no letters, characters or symbols anywhere" |
| Text covers the face | "never covering the face", name the placement |
| Text under app chrome | Keep it out of the top ~12% and bottom ~20% on 9:16 |
| Lockup looks pixelated | Use the vector logo in the edit, not a scaled PNG |
| Copy on screen in all-lowercase or with made-up numbers | Proper grammar and capitalisation; only facts the user supplied |

<!-- Sources: cinematic-story-reel references/prompt-guide.md sections 1, 2, 3, 7, 9 and 10 (tested in an internal test reel); thumbnail SKILL.md and references/concept-frameworks.md (concept method adapted from higgsfield-youtube-thumbnail, MIT); promo-film-rules sections 3, 5, 6 and 9; saas-demo-maker SKILL.md and references/borrow-menu.md; product-shoot references/modes.md (adapted from higgsfield-ai/skills, MIT); game-studio references/sprite-prompts.md; prompt-styles film-stocks.md, atmosphere.md, realism.md (PromptWise free guides, fetched 2026-10-20). -->
