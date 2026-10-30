# Ads, promos, launch films, SaaS demo ads (generation lessons)

This file holds only the prompting and generation lessons from real ad builds. Every rule below was a real rejection in a review round (the source names the round). Story structure, pacing, edit grammar and the build workflow are out of scope here.

Markers: **[tested]** = generated and reviewed in a source test reel. **[untested]** = not run in a source test. "(rejected: ...)" = a review round that turned the opposite down.

## Triggers

"product ad", "demo ad", "promo film", "brand film", "launch video", "launch short", "8 second ad", "15 second ad", "SaaS ad", "app promo", "ad for my product with a customer", "the camera angles look weak", "the shots look generic", "it looks soft / low quality".

## Load these

| Need | File |
|---|---|
| World stills, i2v, hidden cuts, grade lock | [cinematic-story.md](cinematic-story.md) |
| The hero, cast bible, sheets | [character-consistency.md](character-consistency.md), [avatar-portrait.md](avatar-portrait.md) |
| The hero speaking on camera | [talking-head-ugc.md](talking-head-ugc.md) |
| Logo, sign, on-screen copy, UI | [text-logo-ui.md](text-logo-ui.md) |
| Product inserts | [product.md](product.md) |
| Look blocks (light, Kelvin, film, realism, motion) | [../styles/README.md](../styles/README.md) |

Router shot types ([../model-router.md](../model-router.md)): `establishing`, `character-performance`, `dialogue-lipsync`, `macro-texture`, `product-motion`, `short-insert`, `character-sheet`, `text-graphic`.

## Recipe

### 1. Write the cast bible once (paste word for word)

Per job: a trait line per character (and pet or prop), SET, LIGHT (Kelvin + source + what is not there), FILM (one stock, different from earlier ads), REALISM, MOTION. Build each from the style files.

### 2. Stills, in this order

| Still | How |
|---|---|
| Character sheet | three panels on grey, 16:9 ([../styles/reference-sheets.md](../styles/reference-sheets.md)), after a casting pass of a few face options picked by taste |
| Logo that says what the business is | text quoted and spelled letter by letter; check spelling |
| Empty set plate | no people; lived-in (bags, notes, clutter of the trade) |
| Opening world shot with the logo on the sign | logo passed as a reference |
| First frames | sheet + set as references; ask for 2 outputs and pick |
| Product outputs and any content shown in the UI | fictional, no real brands |

Check every still at full size (identity, spelling, hands, the angle you planned) before animating.

### 3. Shot language

- **Every live shot has a named, motivated angle**: POV, subject-eye level (pet / dog-eye level), macro, over-the-shoulder, crane, rack focus. No neutral wides. Flat mediums were called weak.
- **Camera grammar comes from the hero's world**: skate = fisheye low follow, wheel-level tracking, snap crash zooms, whip pans; pets = dog-eye level, slow-mo shake; DJ = platter top-down. Don't default to generic cinema moves.
- **Simple, quiet promos are the exception**: intimate, eye-level, shallow focus, slow push-ins. No high crane wides, no fisheye, no whip-pans, no flashes (rejected: "camera angles are shit, feels rushed", autoposting 16 s v1). Pick per brief.
- **Hook in 1 to 2 s is an event, not a title**: something happens to a person or the world (a pratfall, a plug snapping, a flame flaring). The first frame is never a product-UI frame.
- **The hero's signature physical action is the product action** (a punch is the click, a shake is the burst, a wipe is the reveal). Write that action as the shot's one beat.
- **Generate native to the target aspect.** Never letterbox 16:9 into 9:16.

Prompt-able camera menu (from reference-film breakdowns):

| Shot | Use for |
|---|---|
| Fast push-in from a wide establishing shot to the hero (0.8 s, ease-out) | hook / world intro |
| Low wide, 18-24 mm, close to the counter or floor; the hero leans toward the lens | problem / talking beats |
| High drone wide of the lone business (empty lot) | "nobody knows I exist" |
| Laptop POV from behind the screen (lid in the lower third) | before cutting to UI |
| Macro insert, shallow depth of field (a fingertip on a key) | proof / commitment |
| Selfie-arm walk-and-talk, wide lens | insight / humour |
| FPV forward chase over ground or water through a doorway | hook one-take |
| Overhead 90° → crane down + pitch up | "before" state hook |
| Low-angle symmetric hero shot walking to camera | climax |
| Rack focus from hero to phone | result |
| Behind-the-head orbit into black (two shots joined by ~3 black frames) | before → after time skip |
| Ceiling tilt-down reveal inside a generated space: "camera starts on ceiling lamps, tilts down to reveal..." | output becomes reality |
| Whip-pan with motion blur | montage joins |

### 4. Video generation settings that mattered

- One model for all live shots unless the user says otherwise (the source builds used Seedance 2.x at 720p; see [../models/seedance.md](../models/seedance.md)). First frame only from a checked still.
- 720p upscaled to 1080p read soft in one review (rejected). For hero shots: generate at 1080p, or use high-resolution stills with slow camera moves. Say when a render is upscaled.
- Put spoken lines in quotes in the prompt. The hero speaks on camera (1 to 2 short lines); a whisper's word ends run short, so leave the full audio tail when cutting.
- Slow motion is written as a generated ramp, never a stretch in the edit ([../styles/motion-shutter.md](../styles/motion-shutter.md)).
- An object on the lens (a bee, a drop) must be in sharp focus with visible detail; prompt the focus pull explicitly (rejected: a blurry blob).
- Fix a weak shot in the edit first (punch-in, overlay, speed). Re-shoot only if the edit cannot.

### 5. Product UI and on-screen text

- Do not generate the product UI in video. Screens in live shots are "an even cool white glow" [tested]; product beats are designed motion graphics built in the edit.
- No fake app chrome (sidebars, nav, settings rows). No real app UI screenshots unless asked.
- Social mockups must look like the real app UI. Never crop post images in grids; show full posts.
- Continuity: if the hero uploads a photo, it is the photo they took earlier in the film. Generate it once and reuse the file.
- On-screen copy: proper grammar and capitalisation, no unverified numbers ("Trained on N ads" was cut). Only facts the user supplied.
- Product UI accent colors stay the product's own brand color, even on the hero's canvas.

### 6. Never reuse

Never reuse an earlier ad's look, hero, business, music track or payoff shape. Name 3 overused ideas in the product's category before writing prompts, and use none of them. No dull example businesses (a bakery was rejected); pick a hero with visual edge.

### Filled example (live shot, i2v, 5 s)

Context: a dog-grooming salon owner; the dog's shake is the product's "burst of outputs" moment.
```
@Image1 is the first frame; preserve the groomer and the wet grey terrier exactly. Dog-eye-level low shot, 24 mm lens, close to the tiled floor. 0-1.5s: the terrier stands dripping in a steel tub, ears flat, the groomer in a teal apron leans in behind it. 1.5-3.5s: the dog shakes hard, water drops spray toward the lens, each drop a crisp separate bead lit from behind by the window. 3.5-5s: one drop hits the lens and stays sharp with a bright highlight; the groomer laughs and says "Every single time." One slow push-in toward the dog from start to end. Daylight from the window behind the tub, about 5600 Kelvin, is the only strong light: it backlights the spray and leaves the corners in soft shadow. No text, no subtitles, no watermark.
```

## Pitfalls → fixes

| Pitfall (rejected in review) | Fix |
|---|---|
| Flat mediums, neutral wides | A named, motivated angle per shot from the hero's world |
| Generic cinema moves | Camera grammar from the hero's world |
| Soft, upscaled-looking footage | 1080p for hero shots, or high-res stills with slow moves |
| Rushed, harsh camera on a calm promo | Eye-level, shallow focus, slow push-ins; no whips or flashes |
| Opens on a title or a UI frame | Open on an event in the hero's world in 1 to 2 s |
| Generic logo | A logo that says what the business is; spelled letter by letter |
| Logo looks pixelated in the lockup | Vector logo in the edit |
| UI garbled in a video | Screens as a cool white glow; UI built in the edit |
| Fake app chrome | Free-floating designed cards in the edit |
| Blurry object on the lens | Sharp focus with visible detail, prompt the focus pull |
| Face drifts across the ad | Character sheet + identity still; wardrobe and props as backup |
| Look copied from an earlier ad | New film stock, palette, hero and payoff each time |
| Invented numbers on screen | Only facts from the user |
| 16:9 letterboxed into 9:16 | Generate native to the target aspect |

<!-- Sources: promo-film-rules SKILL.md sections 1 (camera-angle rules only), 3, 4, 5, 6, 8 and 9 (Nightjar promo v1-v5, ROLLA 15 s, SCORCH 20 s, SOAK 8 s, autoposting 16 s v1, AI Twin demo round 2); saas-demo-maker SKILL.md Rules (Camera and edit, Generation, Copy) and Step 4, references/borrow-menu.md sections 1, 7 and 10, references/build-kit.md gotchas; cinematic-story-reel references/prompt-guide.md (UI glow, tested). Model ids from the sources replaced with human model names; provider tool names removed. -->
