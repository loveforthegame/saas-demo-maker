# Look and style library

A style is a block of words that names a physical cause and the visible result. Every file here follows one rule: **name the real thing, then say what the viewer sees.** "f/1.4" alone is a weak hint. "85 mm at f/1.4, only her eyes sharp, the lanterns melt into round circles of light" is a picture the model can copy.

These blocks are provider-neutral. They describe a look, not a model. Model syntax (reference tags, option names, durations, negative-prompt rules) lives in `../models/<family>.md`. Which model to use lives in `../model-router.md`.

Load only the file for the look you need.

## Style router

| The shot needs / the problem is | Load |
|---|---|
| Space, layers, foreground framing, still-then-animate workflow, parallax | [depth.md](depth.md) |
| Where the light comes from (front, side, back), hard vs soft shadows, one-light rule, catchlights | [light-direction.md](light-direction.md) |
| Warm vs cold light, Kelvin numbers, "night looks like day", mixed warm inside / cold outside | [color-temperature.md](color-temperature.md) |
| Background blur, bokeh, deep focus, rack focus | [aperture.md](aperture.md) |
| Motion blur, frozen action, slow motion, speed ramp, time-lapse, phone look, "looks like a video game" | [motion-shutter.md](motion-shutter.md) |
| Film look, grain, color cast, black and white, neon halation, "looks like a phone" | [film-stocks.md](film-stocks.md) |
| Haze, god rays, dust motes, embers, backlit rain, "looks like CGI", "the air is empty" | [atmosphere.md](atmosphere.md) |
| Waxy skin, glowing eyes, frozen people, sweat, macro proof shots, one consistent multi-shot scene | [realism.md](realism.md) |
| Character or prop reference sheets for consistency | [reference-sheets.md](reference-sheets.md) |

### Named looks → files

| Someone asks for | Stack these |
|---|---|
| "Make it look like film" | film-stocks (one stock) + motion-shutter (film blur) + realism |
| "Night looks like day" | color-temperature (8000 K or the named practical) + light-direction (one light) |
| "Looks like CGI / too clean" | atmosphere (one air, backlit) + film-stocks + realism |
| "Looks like a video game" (motion) | motion-shutter (film blur), remove "smooth" |
| "Background still sharp" | aperture (f/1.4 or f/2.8 with bokeh sources) |
| "Everything in focus" | aperture (f/8 or f/16), delete saved "shallow depth of field" lines |
| "Add god rays" | atmosphere (haze, source behind, something breaking the light) |
| "Fake-looking skin / plastic people" | realism block + light-direction one-light rule |
| "Keep the character consistent" | reference-sheets + realism (CAST and REFERENCES rules) |
| "Phone footage / UGC look" | motion-shutter (phone video block) |
| "Noir" | film-stocks (Ilford HP5) + light-direction (one hard light) |
| "Neon night street" | film-stocks (CineStill 800T) + atmosphere (backlit rain) |
| "Candlelit" | color-temperature (2700 K) |
| "Slow-mo moment" | motion-shutter (slow motion or speed ramp) |
| "Cinematic depth / layered frame" | depth + aperture |

Styles stack. A typical cinematic shot uses one block each from light, color temperature, aperture, motion and film stock, plus the realism block. Keep one block per category: two light blocks or two film stocks fight each other.

## Universal style rules (from all nine guides)

1. **Number + source + result.** Write the setting (Kelvin, f-stop, shutter, stock name), the real source it comes from (candle, 85 mm lens, 1/1000 shutter, Kodak Portra 400), and what is visibly sharp, blurred, warm, glowing. The result sentence does most of the work.
2. **Kill empty boosters.** "Cinematic lighting", "moody", "atmospheric", "vintage filter", "smooth motion", "8k", "ultra detailed", "hyper-realistic", "flawless", "masterpiece" push toward the clean digital/CGI look or describe a feeling the model cannot draw. Replace each with a physical cause.
3. **Rule out what isn't there.** End light and air lines with the sources you don't want: "No daylight, no blue light", "no torches, no lanterns", "No golden-hour warmth". Models add lights you never asked for. (Some models handle "no X" badly; the model file says when to turn these into positive statements.)
4. **Same line, word for word, every shot.** The light line, film line, air line and CAST line are pasted unchanged into every shot and take of a scene. Paraphrase or omission drifts back to neutral and the cut jumps.
5. **One main of each.** One main light (any second light clearly weaker), one main air, one film stock, one focus target, one camera move, one action per short shot.
6. **Still first, then animate.** Make the image, check it at full size (whites for color, shadow edges for light, skin/eyes/hands for realism, the focus plane), then use it as the first frame and keep the same style lines in the video prompt. The video prompt then describes only motion, camera, change and sound.
7. **Check your saved style lines for conflicts.** A habitual "shallow depth of field" kills f/16; "smooth motion" kills film blur; "cinematic lighting" kills a named source.
8. **Fix one thing at a time.** Change one block, regenerate, compare. Results vary per model and per take; generate a few.

## Standard video prompt skeleton

Every long-form video prompt in the guides uses this block order. Use it, then paste style blocks into their slots.

```
REFERENCES: image 1 is the [PERSON A], image 2 is the [location]. Keep each face, hairstyle and outfit exactly as in its image.
SET: [place, materials, anything that moves]. No readable text, signs or logos.
LIGHT: [paste light / color-temperature / air line]
MOTION: [paste motion block, if a motion look is needed]
FILM: [paste film line, if a stock is used]
CAST:
- [NAME IN CAPS]: [age, face, hair, outfit]. Voice: [voice].
A scene from a modern cinematic short film, shot at 24 fps. It is one continuous shot. / It has [n] shots separated by hard cuts.
SHOTS (seconds):
0.0-3.0 SHOT 1. [SHOT SIZE], [lens] mm at [f-stop], [one camera move]: [action with timings "at about 1.5 s"]. [Repeat the key visible result: what blurs, what glows, what stays sharp.]
SOUND: [real sounds of the place]. Nobody says anything that is not written here. No music, no narration.
LOOK: [palette, contrast, depth of field]. Natural movement, breathing and blinking, no frozen poses. Real unretouched skin, hands with five fingers. No text, subtitles, captions, logos or readable signs anywhere. No slow motion [unless the shot asks for it].
```

Image prompt skeleton:
```
Photorealistic [shot size] of [subject] [one action] in [place, time of day]. [Camera height, direction, distance], [focal length] mm lens at [f-stop]. [Light line]. [Air line, optional]. Shot on [film stock], 35mm film: [look words] (optional). [Realism block]. No readable text, signs or logos.
```

## How to inject a block into a model's slot order

Each model file in `../models/` gives its own slot order (for example: subject → action → scene → camera → light → style, or a labeled block list). The style blocks here do not change that order. They fill slots:

| Style file | Goes into the slot named |
|---|---|
| light-direction, color-temperature | LIGHT (or the "lighting" position in the model's order) |
| atmosphere | LIGHT AND AIR, right after the light line |
| aperture, depth | the camera / lens position, or the SHOT line |
| motion-shutter | MOTION, near the top, and its key result repeated in the SHOT line |
| film-stocks | FILM, or the style / look position |
| realism | the end of an image prompt; the LOOK line of a video prompt |
| reference-sheets | a separate generation; its output becomes a reference image |

Steps:
1. Write the brief (`../brief-schema.md`) and pick the model (`../model-router.md`).
2. Open the model file and take its slot order and syntax (reference tags, negative prompt field or not, max length).
3. Paste each chosen block into the matching slot, word for word.
4. If the model is short-prompt (some image and fast video models), keep the number + source + one result sentence and cut the rest.
5. If the model turns "no X" into X, rewrite each "No ..." tail as a positive statement ("the sky is deep blue-black" instead of "no daylight").
6. For image-to-video, drop the look blocks the first frame already carries; keep only light changes, motion and sound.

Division of labor: model files own syntax, reference tags, option names and durations. This folder owns the words that describe a look.

## Self-check before sending

- Every style block has a number or name AND a visible result sentence?
- Boosters ("cinematic", "8k", "moody", "vintage", "smooth") removed?
- Light line ends with what light is NOT there (or the positive version on models that need it)?
- Style lines identical across all shots of the scene?
- Only one block per category, no conflicting saved lines?
- Image-first path planned for anything expensive?

<!-- Distilled from the prompt-styles skill, which came from the PromptWise / AI Video Bootcamp free guides (promptwise-free.vercel.app/2, 15, 16, 17, 18, 22, 23, 24, 25), fetched 2026-10-20. Pages 3-13 and 19-21 returned 404; page 14 duplicates page 2. -->
