# Character consistency across shots

Markers: **[tested]** = generated and reviewed in a source test reel. **[untested]** = not run in a source test. Unmarked = the source gave no status.

## Triggers

"keep the character consistent", "same character in every shot", "same person, new scene", "character bible", "the face keeps changing", "recurring mascot", "series with the same host", "put my character in a new world", "another angle of the same shot", "same outfit every time", "sprite frames don't match".

## Load these

| Need | File |
|---|---|
| Three-panel character sheet, prop sheet, face edit | [../styles/reference-sheets.md](../styles/reference-sheets.md) |
| CAST and REFERENCES rules, one consistent multi-shot scene | [../styles/realism.md](../styles/realism.md) |
| Rule 4: the same line word for word in every shot | [../styles/README.md](../styles/README.md) |
| The person itself | [avatar-portrait.md](avatar-portrait.md) |
| Stylized characters and sprite frames | [stylized-anime-pixel.md](stylized-anime-pixel.md) |

Router shot types ([../model-router.md](../model-router.md)): `character-sheet`, `hero-still`, `identity-locked-motion`, `multi-shot-sequence`. Brief fields: `cast.trait_line`, `references` in [../brief-schema.md](../brief-schema.md).

Model notes: Nano Banana Pro held face, hair and outfit 7/7 across i2i worlds [tested] ([../models/nano-banana.md](../models/nano-banana.md)). Multi-reference identity and garment hold: also Nano Banana Pro (product try-on source). Video identity from a first frame: Seedance 2.0 i2v [tested], Veo 3.1 Fast for talking clips [tested]. Kling 3 Pro start + end image for body moves [untested] ([../models/kling.md](../models/kling.md)).

## Recipe

### 1. Write the character bible once

```
Name (internal only): {name}
Trait line (paste word for word in EVERY prompt, never paraphrase):
  {age range} {gender presentation} with {hair colour, length, style}, {skin tone}, {one distinctive mark or accessory},
  wearing {one outfit with colours}
Accent object (the visual metaphor, recurs in most shots): {object} in {brand accent colour}
Look line (paste word for word in every still and video prompt): {light}, {shadow tint}, {grain}, {lens feel}
Voice block (talking formats only): {voice type}, {accent}, {pace ~2.7 words per second}, {energy}, same mic distance,
  same voice in every clip
Never: {what must not change, e.g. no hat, sleeves down}
```

Rules [tested]: one mid-tone outfit color (not black on a dark set, it merges); a plain uncluttered band where text will go; the accent object in the brand color doubles as the grade anchor.
Brief-schema rule: trait lines are 6 to 10 concrete, visible traits. Never a name alone, never "same as before".

### 2. Make the sheet and the identity still

1. Character sheet (three panels on grey) from reference-sheets.md. Prop sheet for any recurring object.
2. Hide the face in the front full-body panel so the close-up is the only detailed face.
3. Identity still (avatar-portrait.md step 5) [tested pattern].
4. Check sharpness, matching outfit and materials, complete framing, at full size.

### 3. Same character in a new world (i2i) [tested pattern, 7/7 kept face, hair and outfit]

Reference = the identity still.
```
The same {person word} as image 1: {trait line}. {Shot size + angle}: {action} in {world}. {Where the subject sits in frame + where the clean space is}. {Look line}, {lens feel}, shallow depth of field. {Aspect word}. No text, no logos.
```
- Always i2i from the ORIGINAL identity still, never from a sibling world still. Drift compounds.
- One action per still, written as the frame the motion starts from.
- Put the accent object in most worlds; it carries the metaphor and holds the grade together.

### 4. Reframe for a second angle (i2i) [tested]

```
The same {person word} as image 1, same outfit, same room and the same light. Reframe {new size}, camera {N} degrees to the {side}, {face to the lens}. {Text zone still clear}. {Look line}. Photorealistic, no text, no logos.
```
A 20-degree turn came out as an offset framing, not a turn [tested]. Ask for the framing you want to see, not the degrees.

### 5. One consistent multi-shot scene

1. Make the empty set (no people).
2. Make one still per character in the same light.
3. Attach in a fixed order; keep CAST and LIGHT lines word for word.

```
REFERENCES: image 1 is [PERSON A], image 2 is [PERSON B], image 3 is [the location]. Keep each face, hairstyle and outfit exactly as in its image in every shot.
SET: [the location, its main objects and materials]. No signs, posters or readable text anywhere.
LIGHT, identical in every shot: [one light source] throws [warm amber] light on the faces, and the rest of the [room] falls into deep [color] shadow. The same color palette, contrast and exposure in every shot, so all shots match as one continuous scene.
CAST:
- [PERSON A]: [age, look and clothing]. Voice: [voice].
- [PERSON B]: [age, look and clothing]. Voice: [voice].
A scene from a cinematic short film, shot at 24 fps. It has [number] shots separated by hard cuts.
SHOTS (seconds):
0.0-3.0 SHOT 1. [SHOT SIZE], [lens]: [what happens]. [PERSON A]: "[line]"
3.0-5.0 HARD CUT. SHOT 2. [SHOT SIZE], [lens]: [what happens].
SOUND: only the characters' own voices, close and clear, lips matching every word; [three or four real sounds of the place]. Nobody says anything that is not written here. No music.
LOOK: [one light source] with deep [color] shadows, warm natural skin tones and shallow depth of field. Every character keeps moving naturally, breathing and blinking, with no frozen poses. Real unretouched skin, hands with five fingers. No text, subtitles, logos or readable signs.
```
- Names in CAPITALS, identical in every line. Use the model's reference tag syntax in REFERENCES ([../models/](../models/)).
- Too long for one take: split the shot list, restart timings at 0.0, keep REFERENCES/SET/LIGHT/CAST identical.
- Multi-shot labels with the trait and look lines in every shot: see [cinematic-story.md](cinematic-story.md) [untested].

### 6. Re-anchoring rules

| Situation | Re-anchor with |
|---|---|
| Every new still | The original identity still (and sheet), never the last generated still |
| Every video shot | A checked still as the first frame + the trait line word for word |
| A real person's face | The face-lock line from [avatar-portrait.md](avatar-portrait.md), faces first in the reference list |
| A product or prop | `Keep the product exactly as in image 1: shape, label, colors.` (see [product.md](product.md)) |
| A stylized or game character | `Image 1 is the exact character: keep the same silhouette, face, palette, costume, markings, proportions and art style. Change only the pose.` |
| Enemies or props in the same world | The hero as image 2, "style reference only, do not copy the character" |
| A long restyled clip in chunks | Chunk 1's last frame as a style reference for the other chunks |
| A carousel or ad set | Slide 1 as an extra reference: "match the palette, light and grade of image 2" |

Wardrobe and props carry continuity as a backup when the face drifts (borrow-menu rule).

### Filled example (i2i, new world)

```
The same man as image 1: a man in his early forties with short salt-and-pepper hair and a trimmed beard, light olive skin, a thin silver ring in his left ear, wearing a rust-orange canvas work jacket over a grey henley. Low-angle medium shot: he steps off a ferry ramp onto a wet concrete pier at dawn, carrying the teal thermos. He sits on the left third of the frame; the right half is open grey sea and sky for text. Low warm sun behind him, cool blue shadows, fine film grain, 35mm lens feel, shallow depth of field. Vertical 9:16. No text, no logos.
```
(The teal thermos is the accent object. The trait line is pasted unchanged from the bible.)

## Pitfalls → fixes

| Pitfall | Fix |
|---|---|
| Face drifts between shots | i2i from the original identity still; trait line word for word [tested] |
| Drift grows shot by shot | Stop chaining stills; go back to the original every time |
| Outfit details change | Repeat the outfit colors in the trait line; add a "Never:" line; use the sheet |
| Two faces compete on the sheet | Hide the face in the full-body panel |
| Turn request gives an offset framing | Describe the framing you want to see [tested] |
| Light color changes between shots | "LIGHT, identical in every shot" + the same palette/contrast/exposure line |
| Names drift ("the detective", "he", "Marcus") | One CAPS name, identical in every line |
| Sprite size changes between frames | Master frame as image 1 in every call; "Same character size and camera distance in every cell" |
| Restyled chunks drift (hair color, line weight) | Chunk 1's last frame as style reference; same prompt, model and settings for all chunks |

<!-- Sources: cinematic-story-reel references/prompt-guide.md section 2 (character bible, identity still, i2i new world, reframe; tested in an internal test reel); prompt-styles reference-sheets.md and realism.md (PromptWise free guides, fetched 2026-10-20); game-studio references/sprite-prompts.md (identity lock across frames); product-shoot SKILL.md and references/modes.md (fidelity sentence, carousel lock; adapted from higgsfield-ai/skills higgsfield-product-photoshoot, MIT); anime-me SKILL.md (long-clip chunks); saas-demo-maker references/borrow-menu.md rule 10. -->
