---
name: prompt-styles
description: >-
  Library of cinematic prompting styles for AI image and video: depth layering, light direction and
  hardness, color temperature (Kelvin), aperture and focus, shutter and frame-rate motion looks,
  film stocks, atmosphere (haze, dust, embers, backlit rain), realism (skin, eyes, sweat, breathing)
  and character/prop reference sheets. Each style is a paste-ready block plus a template, the
  WEAK-to-BETTER rewrite, where it fails and a fix table. Built to be injected into other prompting
  skills (predis-prompting, predis-director, video-to-superprompt, ugc/remix/replica prompt skills).
  Use when: a prompt needs a specific look ("make it look like film", "night looks like day",
  "looks like CGI / a video game", "background still sharp", "add god rays", "fake-looking skin",
  "keep the character consistent"); writing a style block into a shot; another prompting skill
  asks for a look block.
  NOT for: per-model syntax, reference tags or option names (predis-prompting); picking a model or
  running a job (predis-generate).
---

# Prompt Styles

A style is a block of words that describes a physical cause and the visible result. Every style in this library follows the same rule: **name the real thing, then say what the viewer sees.** "f/1.4" alone is a weak hint; "85 mm at f/1.4, only her eyes sharp, the lanterns melt into round circles of light" is a picture the model can copy.

Load only the reference file for the style you need.

## Style router

| The shot needs / the problem is | Load |
|---|---|
| Space, layers, foreground framing, image-then-animate workflow | [references/depth.md](references/depth.md) |
| Where light comes from (front/side/back), hard vs soft shadows | [references/light-direction.md](references/light-direction.md) |
| Warm vs cold light, night looks like day, mixed warm/cold | [references/color-temperature.md](references/color-temperature.md) |
| Background blur, bokeh, deep focus, rack focus | [references/aperture.md](references/aperture.md) |
| Motion blur, frozen action, slow motion, speed ramp, time-lapse, phone look, "looks like a video game" | [references/motion-shutter.md](references/motion-shutter.md) |
| Film look, grain, color cast, black and white, neon halation, "looks like a phone" | [references/film-stocks.md](references/film-stocks.md) |
| Haze, god rays, dust motes, embers, backlit rain, "looks like CGI" | [references/atmosphere.md](references/atmosphere.md) |
| Waxy skin, glowing eyes, frozen people, sweat, macro proof, multi-shot consistent scene | [references/realism.md](references/realism.md) |
| Character or prop reference sheets for consistency | [references/reference-sheets.md](references/reference-sheets.md) |

Styles stack. A typical cinematic shot uses one block each from light, color temperature, aperture, motion and film stock, plus the realism block. Keep one block per category: two light blocks or two film stocks fight each other.

## Universal style rules (from all nine guides)

1. **Number + source + result.** Write the setting (Kelvin, f-stop, shutter, stock name), the real source it comes from (candle, 85 mm lens, 1/1000 shutter, Kodak Portra 400), and what is visibly sharp, blurred, warm, glowing. The result sentence does most of the work.
2. **Kill empty boosters.** "Cinematic lighting", "moody", "atmospheric", "vintage filter", "smooth motion", "8k", "ultra detailed", "hyper-realistic", "flawless", "masterpiece" push toward the clean digital/CGI look or describe a feeling the model cannot draw. Replace each with a physical cause.
3. **Rule out what isn't there.** End light/air lines with the sources you don't want: "No daylight, no blue light", "no torches, no lanterns", "No golden-hour warmth". Models add lights you never asked for.
4. **Same line, word for word, every shot.** The light line, film line, air line and CAST line are pasted unchanged into every shot and take of a scene. Paraphrase or omission drifts back to neutral and the cut jumps.
5. **One main of each.** One main light (any second light clearly weaker), one main air, one film stock, one focus target, one camera move, one action per short shot.
6. **Still first, then animate.** Make the image, check it at full size (whites for color, shadow edges for light, skin/eyes/hands for realism, focus plane), then use it as the first frame and keep the same style lines in the video prompt. Video prompt then describes only motion, camera, change and sound.
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

## How to inject into another prompting skill

Add this section to the host skill (for example `predis-prompting/SKILL.md`, after its universal rules):

```markdown
## Look and style blocks
For any named look (light direction, Kelvin, aperture, shutter/slow-mo, film stock, haze/dust/embers/rain, skin realism, reference sheets), load the matching file from the `prompt-styles` skill router and paste its block into the SET/LIGHT/MOTION/FILM/LOOK slot. Keep the model-specific syntax from this skill; take the look wording from prompt-styles.
```

Division of labor: the host skill owns model syntax, reference tags, option names and durations. This skill owns the words that describe a look.

## Self-check before sending

- Every style block has a number or name AND a visible result sentence?
- Boosters ("cinematic", "8k", "moody", "vintage", "smooth") removed?
- Light line ends with what light is NOT there?
- Style lines identical across all shots of the scene?
- Only one block per category, no conflicting saved lines?
- Image-first path planned for anything expensive?

<!-- Distilled from the PromptWise / AI Video Bootcamp free guides (promptwise-free.vercel.app/2, 15, 16, 17, 18, 22, 23, 24, 25), fetched 2026-10-20. Pages 3-13 and 19-21 returned 404; page 14 duplicates page 2. -->
