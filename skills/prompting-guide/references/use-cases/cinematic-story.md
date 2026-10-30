# Cinematic story shots: world stills, image-to-video, hidden cuts, multi-shot, grade lock

Markers: **[tested]** = generated in an internal test reel and reviewed. **[untested]** = from reference-reel breakdowns or model docs, never run in that test. Unmarked = the source gave no status.

## Triggers

"cinematic shot", "story reel", "short film shot", "AI art video", "first frame", "world still", "animate this image", "image to video", "camera move", "reveal shot", "transition between shots", "hidden cut", "seamless transition", "multi-shot", "trailer", "montage", "keep the grade the same", "the camera ignored my move", "the model cut on its own", "the shot is too still".

## Load these

| Need | File |
|---|---|
| Layers, foreground framing, parallax | [../styles/depth.md](../styles/depth.md) |
| One light, hard/soft, direction | [../styles/light-direction.md](../styles/light-direction.md) |
| Kelvin, night that looks like night | [../styles/color-temperature.md](../styles/color-temperature.md) |
| Focus, bokeh, rack focus | [../styles/aperture.md](../styles/aperture.md) |
| Film blur, frozen, slow motion, ramp, time-lapse | [../styles/motion-shutter.md](../styles/motion-shutter.md) |
| Film stock, grain | [../styles/film-stocks.md](../styles/film-stocks.md) |
| Haze, dust, embers, backlit rain | [../styles/atmosphere.md](../styles/atmosphere.md) |
| People that move like bodies | [../styles/realism.md](../styles/realism.md) |
| Recurring character | [character-consistency.md](character-consistency.md) |
| Video prompt skeleton and slot order | [../styles/README.md](../styles/README.md) |

Router shot types ([../model-router.md](../model-router.md)): `establishing`, `hero-still`, `character-performance`, `identity-locked-motion`, `multi-shot-sequence`, `long-take`, `fast-action`, `short-insert`, `macro-texture`, `restyle`, `extend`.

## Model pick per shot type (from the source test reel)

Confirm the model exists on your provider and read its model file before writing. If the first pick is missing or fails twice, use the fallback.

| Shot type | First pick | Why | Fallback | Status |
|---|---|---|---|---|
| Identity still, world stills, first frames | Nano Banana Pro | holds a face across i2i worlds, renders quoted text | cheaper Nano Banana tier for drafts | [tested] |
| Story shot with one camera move (i2v, 4 s) | Seedance 2.0 at 720p | followed every camera move asked, 7/7 usable | Kling 3 Standard start+end; Seedance 2.0 Fast for drafts only | [tested] |
| Reveal with a designed end frame | Seedance 2.0 first + last frame | both ends of the move are locked | Kling 3 Standard start + end | [untested] |
| Multi-shot run (montage, trailer, coverage) | Seedance 2.0 multi-shot with `Shot N:` labels | cuts follow labels, grade persists | Kling 3 Pro multi-shot | [untested] |
| Hero shot that must be sharp at 1080p | Seedance 2.0 at 1080p | native detail | 720p + lanczos upscale + grain (was acceptable) | [tested] (upscale route) |
| Talking clip / voiceover line | Veo 3.1 Fast, audio on, 8 s | identity held 3/3, line came back word for word | Veo 3.1 for a final take | [tested] |
| Cheap insert: macro press, time-lapse, prop drop | Seedance 1.5 Pro | good single beats for little spend | Kling 2.5 Turbo | [tested] |
| Body physics (turn, fall, outfit morph) | Kling 3 Pro start + end image | cleaner body moves | Seedance 2.0 first + last | [untested] |
| One-change twin of a clip (mood, weather, object) | Gemini Omni Flash v2v | frame-locked, cheap | Wan 2.7 video edit | [untested] |
| Restyle of a real take | Kling 3 Omni | keeps motion, takes a look reference | Runway Aleph 2 | [untested] |
| Short exit or whip-turn stare | MiniMax Hailuo H3 Max | cheap short beats | Seedance 2.0 i2v | [untested] |
| Native music bed or SFX | Seedance 2.0 or Veo 3.1 with audio on | audio made with the picture | a licensed track from the user | [untested] |

Model files: [seedance](../models/seedance.md), [veo](../models/veo.md), [kling](../models/kling.md), [minimax-hailuo](../models/minimax-hailuo.md), [gemini-omni](../models/gemini-omni.md), [wan](../models/wan.md), [nano-banana](../models/nano-banana.md), [video-edit-restyle](../models/video-edit-restyle.md).

A later note from a promo build: 720p upscaled to 1080p was called soft in one review. For hero shots, generate at 1080p, or use high-resolution stills with slow camera moves.

## Recipe

### 1. Lock the look line and the trait line

One look line, word for word, in every still and video prompt: `{light}, {shadow tint}, {grain}, {lens feel}`. Build it from the style files (one light, one Kelvin, one stock). One accent-color object in most shots holds the grade together. Trait line per character: see [character-consistency.md](character-consistency.md).

### 2. Write each world still as the first frame of its move

Not the most beautiful moment:
- Reveal (pull-back): subject 35-45% of frame height, the reveal NOT visible yet (fog, sky, wall behind).
- Push-in: subject small, the detail you will land on visible and lit.
- Object to lens: the object visible near the subject, on a path toward the camera.
- Time-lapse: locked-off, empty sky band, no people moving.
- Product insert: screens are "an even cool white glow" (real UI goes in during the edit; video models garble UI text).

Use the image skeleton from [../styles/README.md](../styles/README.md) and the depth template (foreground element near the lens, subject beyond, background behind). Check the still at full size before animating.

### 3. Image-to-video motion prompt [tested, 7/7 usable]

```
@Image1 is the first frame; preserve {who/what} exactly. {beat-by-beat action with seconds}. {one camera move with start and end}. {optional in-camera transition with its second}. {Look line}. No text, no subtitles, no watermark.
```
(`@Image1` is one tag style; use the model's own first-frame syntax.)

- Beat-by-beat seconds: `0-1s: hold on {action}. 1-4s: {move + what is revealed}. Ends {final framing}.`
- One camera move per shot with a start and an end: "one smooth continuous pull-back and rise ... ends as a wide shot, the subject small in the centre".
- 4 s is plenty [tested]: the edit used 1.1-2.1 s of each shot, often sped 1.4-2.2x. Put the strongest moment at 1-3 s.
- Hold mode (the still is the moment): 3-4 micro-actions (blink, breath, hair drift, glance), "stays seated; does not stand".
- React mode (something happens): give the key beat at least 2 s.
- The image carries look, light and composition. The video prompt adds only camera motion, action, movement in the existing environment, and sound. Add "Preserve the setting and light direction" or "Keep the focus exactly as it is in the image."
- Parallax line that sells depth: "the nearby doorframe shifts more than the distant shelves."

Camera moves that worked [tested]: pull-back and rise to a wide reveal; tracking behind a running subject; straight-up crane away from a top-down subject; quarter orbit while objects lift; rack focus as a small object comes alive and leaves; locked tripod time-lapse (clock spins, sky day to dusk); slow low-angle push-in with an object drifting past the lens.

### 4. In-camera transitions (hidden cuts) [first one tested, rest untested]

| Transition | Phrase | Edit cut point |
|---|---|---|
| Object hits the lens [tested] | `the {accent object} swoops at the lens and fills the frame at {3.4}s` | the fully covered frame |
| Foreground wipe | `a blurred {foreground object} crosses the lens at {t}s, filling the frame` | the covered frame |
| Whip past subject | `at {t}s the camera whips {right} past {subject}'s hair into {next view}` | mid-blur |
| Dive into cloud | `the camera dives into {cloud/haze}, the frame fills with soft {colour} haze at {t}s` | the flat haze frame |
| Fly through glass | `a glass {sphere/window} drifts into the lens; the camera passes through its refraction at {t}s` | the refraction frame |
| White flash | `a lightning flash lights the whole frame at {t}s` | the brightest frame |
| Subject exits | `{subject} is yanked up out of frame at {t}s, leaving the empty {place}` | 3-6 empty frames after |
| Behind-the-head time skip (from a reference-film breakdown) | two shots: A ends with the camera passing behind the head into darkness; B starts in darkness behind a head | join with ~3 black frames |

An object on the lens must be in sharp focus with visible detail; prompt the focus pull explicitly (a blurry blob was rejected in a promo review).

### 5. Multi-shot runs [untested in the test reel]

```
Shot 1 (0-4s): {size}, {move}. {trait line} {action}. {sound}.
Shot 2 (4-8s): {size}, {move}. {trait line} {action}. {sound}.
Shot 3 (8-12s): ...
{Look line}, every shot.
```
Sizes never repeat back to back. Repeat the trait and look lines in every shot. 4-6 s per shot. For the long-form version with REFERENCES/SET/LIGHT/CAST/SHOTS/SOUND/LOOK, use the skeleton in [../styles/README.md](../styles/README.md).

### 6. First + last frame [untested]

Make both stills (the end still is i2i from the start still, subject in the same screen spot). Prompt only the move between them:
```
@Image1 as the first frame, @Image2 as the final frame. Single continuous take, no cuts. {micro-action}. 0-{h}s: static. {h}-{end}s: {one move}, slow at first then faster, revealing {layer 1}, {layer 2}, {layer 3}, settling into a slow creep.
```

### 7. Grade lock

- One look line, word for word, in every still and video prompt. One accent-color object in most shots.
- Grade again in the edit to match all clips to the hero shot, then one grain pass over the whole render.

### 8. Negatives

Describe what is there instead of naming flaws ("empty sky above the skyline", not "no birds"). Keep only the short constraint tail: stills `No text, no logos, no watermark.`; video `No text, no subtitles, no watermark.`; restyles `no new people or objects, the background stays the same room, same expression`.

### 9. Audio prompts

- Voiceover from the character: [talking-head-ugc.md](talking-head-ugc.md).
- Music bed [untested]: test once before relying on it, cheapest first, on a native-audio model, t2v of a neutral plate: `{plate shot}. Sound: {genre} instrumental music bed, {tempo} BPM, {instruments}, {mood}, no vocals, no lyrics, steady from start to end.` Check for vocals, tempo drift and a clean end. If it fails, ask the user for a licensed track. Never use or quote a real song's lyrics.
- SFX [untested]: `Sound: one soft whoosh at {t}s, then room tone` from a native-audio insert, or an SFX pack.
- Audio does not carry across separate runs: a bed must come from one run or one track.
- For a recorded feel: real sounds of the place + "No music". "Nobody says anything that is not written here."

### Filled example (world still → i2v reveal)

Still:
```
Vertical 9:16 photorealistic medium shot of a young woman in a mustard-yellow raincoat standing on a stone harbour wall at blue hour, seen from slightly below eye level. A coil of wet rope close to the lens frames the lower-left corner. She sits in the middle of the frame, about 40% of frame height. Behind her, thick sea fog hides everything beyond the wall. Cold blue light, about 8000 Kelvin, from the open sky; one warm lantern at her feet, about 2700 Kelvin, lights her face from below. Shot on CineStill 800T, 35mm film: tungsten-balanced, cool teal shadows, a soft red halation glow around the brightest lights only, visible grain. 35mm lens. No text, no logos, no watermark.
```
Video:
```
@Image1 is the first frame; preserve the woman and her yellow raincoat exactly. 0-1s: hold; she lifts the lantern to chest height, breath steaming. 1-4s: one smooth continuous pull-back and rise as the fog thins, revealing a lighthouse on the far rocks and the dark sea; the rope in the foreground slides out of frame faster than the lighthouse moves. Ends as a wide shot, the woman small in the centre, the lantern the brightest point. Cool teal shadows, red halation on the lantern only, visible grain. No text, no subtitles, no watermark.
```

## Pitfalls → fixes

| Symptom | Fix |
|---|---|
| Face drifts between shots | i2i from the original identity still; paste the trait line word for word |
| Camera move ignored | Use the full model, not the fast tier; one move with start and end; shorter clip |
| Model cuts on its own | "single continuous take, no cuts" |
| Shot too still | One physical action + one time cue |
| Subject lost in a wide | A saturated garment or accent object; subject bigger in the end frame |
| UI or text garbled | Screens as "even cool white glow"; real UI in the edit |
| Talking line ends early | 18-22 words, or end with "then smiles and holds still for a beat" |
| Voice drift between clips | Same voice block, back-to-back runs; regenerate the outlier (max 1) |
| Grade flicker | Same look line; grade match in the edit |
| Restyle adds things | "no new people or objects" tail; each variant from the base |
| Looks like a video game | Film blur block; remove "smooth", "clean"; name what blurs |
| Night looks like day | Name the only source + Kelvin; "sky is deep blue-black"; "no daylight" |
| Air fades in video | Still as first frame; "stays the same for the whole shot" |
| Focus wanders | Start from a still, small action, "keep the focus on her eyes for the whole shot" |
| Slowed footage warps | Generate the slow motion, don't stretch it |

<!-- Sources: cinematic-story-reel references/prompt-guide.md sections 1, 3, 4, 6, 7, 8 and 10 (tested baseline: identity held 7/7 across i2i worlds and 3/3 talking clips; beat-by-beat seconds + one camera move followed 7/7 by the i2v model); promo-film-rules sections 8 and 9; saas-demo-maker references/borrow-menu.md (behind-the-head time skip); prompt-styles depth, motion-shutter, aperture, atmosphere, color-temperature, film-stocks (PromptWise free guides, fetched 2026-10-20). -->
