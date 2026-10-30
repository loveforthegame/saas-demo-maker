# Edits and one-change restyles (image and video)

Markers: **[tested]** = generated and reviewed in a source test. **[untested]** = not run in a source test. Unmarked = the source gave no status.

## Triggers

"edit this image", "change only the background", "change the text", "change the expression", "make it winter", "change the season", "set it on fire", "make it night", "restyle this for Christmas", "same shot but rainy", "same clip, different mood", "hide the face in this panel", "fix one thing in this image".

Full style changes (anime, clay, pixel) are in [stylized-anime-pixel.md](stylized-anime-pixel.md).

## Load these

| Need | File |
|---|---|
| The light or season you are changing to | [../styles/color-temperature.md](../styles/color-temperature.md), [../styles/atmosphere.md](../styles/atmosphere.md) |
| Product must stay exact | [product.md](product.md) |
| Face must stay exact | [avatar-portrait.md](avatar-portrait.md) |
| Text edits | [text-logo-ui.md](text-logo-ui.md) |

Router shot types ([../model-router.md](../model-router.md)): `restyle`, `extend`, `motion-transfer`, `hero-still` (image edit).

Model notes (from the source skills): image edits with a reference → Nano Banana Pro; text edits → GPT Image 2 ([../models/nano-banana.md](../models/nano-banana.md), [../models/gpt-image.md](../models/gpt-image.md)). One-change twin of a video clip → Gemini Omni Flash v2v, fallback Wan 2.7 video edit [untested]. Restyle of a real take → Kling 3 Omni, fallback Runway Aleph 2 [untested]. VFX on real footage (fire, winter) → Runway Aleph 2 first. See [../models/video-edit-restyle.md](../models/video-edit-restyle.md), [../models/gemini-omni.md](../models/gemini-omni.md).

## Recipe

### 1. One change at a time

Name the ONE thing that changes and list what stays. Regenerate, compare, then make the next change.

Image edit template:
```
Edit image 1. Change ONLY <the text to read exactly "NEW TEXT" | the expression to <emotion> | the background to <new background> | the rim light colour to <colour>>. Keep everything else exactly the same: face, identity, pose, clothing, logo, composition, lighting, colors.
```

Panel edit (reference sheet face hide):
```
Edit only the front full-body panel. Hide its facial features with a flat grey color matching the backdrop. Preserve the hair, head outline, neck, body and clothes. Leave the close-up portrait and back view unchanged.
```

### 2. Restyle a product image (season or aesthetic)

```
Keep the product exactly as in image 1: shape, label, colors. Restyle image 1 into a {season} {aesthetic} version. Keep the same product placement, camera angle and framing. Change only the surroundings: {new_props}, {new_background}, {new_palette}, {new_lighting}. Product remains the sharpest element. {text_clause}
```
With a clean product photo as image 2, add "product matches image 2 exactly".

### 3. VFX and season changes on video

Say what changes AND what stays.

| Change | Prompt |
|---|---|
| Set it on fire | `Add realistic fire to this video: {what burns, default "the background buildings"} are engulfed in roaring flames with embers, smoke and warm flickering light spilling onto {subject}. {subject} stays unharmed and unchanged. {keep}` |
| Make it winter | `Change the season to deep winter: heavy snow covering the ground and surfaces, snow falling, frosty breath, cold blue daylight, {subject} in the same clothes with snow settling on them. {keep} {extra}` |
| Cyberpunk night | `Transform the setting into a rain-soaked cyberpunk city at night: neon signs in magenta and cyan, wet reflective streets, holographic haze, {subject} lit by neon rim light. No readable text. {keep} {extra}` |

Keep line:
```
Keep the exact motion, timing, camera movement, framing and composition of the original video. Keep each person's pose, gestures and expressions.
```
Restyle tail [from the test-reel guide]: `no new people or objects, the background stays the same room, same expression`.
Make each variant from the base clip, never from a previous variant.

### 4. Long clips in chunks

Each chunk is restyled on its own, so the look can drift between chunks (hair color, line weight, background details). To reduce drift:
1. Restyle chunk 1 first and check it.
2. Run the rest with the SAME prompt, model and settings.
3. If the model takes an image reference, pass chunk 1's last frame as a style reference.
4. Check a frame on each side of every join.

### 5. Put the audio back

Video-to-video output often drops or replaces the sound. Put the original audio back in the edit.

### Filled example (one-change video twin)

```
Change the weather to a light rain shower: fine rain falling at real speed, wet pavement with small puddles that reflect the shop lights, wet hair and a darker wet coat on the man. Keep the exact motion, timing, camera movement, framing and composition of the original video. Keep each person's pose, gestures and expressions. No new people or objects, the background stays the same street, same expression.
```

## Pitfalls → fixes

| Pitfall | Fix |
|---|---|
| Composition changes too much | "identical composition to image 1", fewer new props |
| Product re-lit into another color | "product color unchanged, seasonal light on background only" |
| Face changes during an edit | "Keep everything else exactly the same: face, identity..."; fewer style words |
| Edit adds new things | "no new people or objects" tail |
| Rain added but people stay dry | "wet hair and a wet coat", "rain falling at real speed, no slow motion" |
| Fire touches the person | "{subject} stays unharmed and unchanged"; name what burns |
| Variants drift from each other | Make every variant from the base, not from a variant |
| Chunks drift | Same prompt/model/settings; chunk 1's last frame as style reference |
| Sound is gone | Put the original audio back in the edit |

<!-- Sources: thumbnail SKILL.md edit pass (adapted from higgsfield-youtube-thumbnail, MIT); prompt-styles reference-sheets.md face edit (PromptWise, fetched 2026-10-20); product-shoot references/modes.md restyle mode (adapted from higgsfield-ai/skills, MIT); anime-me SKILL.md and references/style-presets.md (VFX presets, long clips, audio); cinematic-story-reel references/prompt-guide.md sections 1 and 7 (one-change twin and restyle rows, restyle tail). -->
