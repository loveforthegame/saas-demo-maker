# Avatars, AI twins, headshots, realistic people

Markers: **[tested]** = generated and reviewed in a source test reel. **[untested]** = from guides, breakdowns or model docs, not run in a source test. Unmarked = the source gave no status.

## Triggers

"make an avatar", "AI twin", "AI version of me", "headshot", "profile photo", "portrait of a person", "realistic person", "AI influencer / persona", "make a creator", "photoreal woman/man", "the skin looks fake / plastic / waxy", "the eyes look weird", "people look like CGI".

If the person must talk: also load [talking-head-ugc.md](talking-head-ugc.md). If the person recurs across shots: also load [character-consistency.md](character-consistency.md).

## Load these

| Need | File |
|---|---|
| Skin, eyes, sweat, breathing, "write a person", macro proof | [../styles/realism.md](../styles/realism.md) (always) |
| Identity sheet for any later shot | [../styles/reference-sheets.md](../styles/reference-sheets.md) |
| One light with a reason, catchlight check | [../styles/light-direction.md](../styles/light-direction.md) |
| Close-up focus (85 mm f/1.4) or readable room (50 mm f/2.8) | [../styles/aperture.md](../styles/aperture.md) |
| Warm/cold light that matches the place | [../styles/color-temperature.md](../styles/color-temperature.md) |
| Skin-friendly film look (Portra 400) | [../styles/film-stocks.md](../styles/film-stocks.md) (optional) |

Router shot types ([../model-router.md](../model-router.md)): `hero-still` (the portrait), `character-sheet`, `identity-locked-motion` (the avatar moving), `avatar-talking-head` (the avatar speaking), `macro-texture` (skin/eye proof shots).

Model notes: identity stills and i2i worlds held a face best on Nano Banana Pro [tested] ([../models/nano-banana.md](../models/nano-banana.md)); a cheaper Nano Banana tier for drafts. For a face plus readable text (a thumbnail, a poster) see [../models/gpt-image.md](../models/gpt-image.md).

## Recipe

### 1. Decide whose face it is

| Case | What to do |
|---|---|
| The user's own face (AI twin) | Ask for 1 to 3 clear face photos. Pass them first in the provider's reference list. Only the user or someone who agreed. |
| An invented person | Write the person from scratch (step 2). Never base it on a celebrity or public figure. |
| A generic person in a crowd | Short trait line, medium or wide shot, no pores (step 4). |

Face-lock line for a real person's photo (from a thumbnail recipe):
```
CHARACTER 1 is the exact person from image 1: same face shape, eyes, nose, lips, jawline, skin tone, hairline and hair. Do not beautify or restyle the face.
```

### 2. Write a person, not a model

A specific person looks more real than a beautiful one. Give every detail a reason (age, job, their week).

```
Photorealistic [shot size] of a [woman or man] of [age], [what they do], [build], with [skin details], [hair] and [eyes]. [They] wear [clothing, with one sign of wear]. [They] [one simple action] in [location, time of day]. The camera is at [eye level], about [distance] away, framing [them] from the [waist] up on a [50 mm] lens. [One light source] lights [their] face from [direction], with [shadow] around [them]. [Their expression, and why].
```

Pick two or three small details with a cause (from realism.md): sweat at the hairline after a run, flushed cheeks from cold wind, ink on the fingers from daily work, a creased shirt at the end of a long day.

### 3. One light, one lens

- Light: one real source, one direction, one color, a stated falloff. End with "No other light sources and no flat fill light." Catchlight check: one lamp = one small reflection per eye.
- Lens: close-up portrait = 85 mm at f/1.4, about one meter from the face, "focus on her eyes". Waist-up in a place = 50 mm at f/2.8, room "softly blurred but still easy to recognize".

### 4. Realism block, matched to distance

Paste at the end of the image prompt:
```
Real, unretouched photographic skin: natural color variation across the face, a little shine on the forehead and nose, softer texture on the outer cheeks, normal creases under the eyes and real texture on the lips. Hair separates into uneven strands with a few flyaways, and makeup and clothing look lived in. A natural, in-the-moment expression rather than a posed model look. It reads as a frame from a film, not a stock photo or a beauty ad. No skin smoothing, waxy skin, porcelain teeth, glowing irises, uniform pore texture or helmet-like hair.
```
Pores only in close-ups and macro. In medium and wide shots, drop pores; keep "no uniform pore texture".

### 5. The identity still [tested pattern]

Use this when the avatar will be reused (talking clips, new worlds). It leaves a clean text zone.

```
{aspect word} photo for a {destination}. {Trait line}, {pose: waist-up, centred, facing the camera, hands relaxed and visible, mouth closed, eyes to the lens}. {Set that fits the brand tone} with depth and one practical light: {practical}, kept below shoulder height. {Text zone: the top third above the head is a plain uncluttered {wall colour} wall; eyes at about 40% of frame height; nothing above the head}. Soft key 45 degrees camera-left, a subtle warm rim light from behind separating hair and shoulders from the background, background a stop darker than the face. Eye-level 50mm, shallow depth of field. Photorealistic, no text, no logos, no watermark.
```

Trait line rules [tested]: one mid-tone outfit color (black merges into a dark set); a plain uncluttered band where text will go.

### 6. Check at full size before anything else

Skin (waxy? pattern?), eyes (one catchlight, no glow, a little redness in the white is fine), teeth, hands (five fingers, one simple action), hair edges. A waxy still stays waxy in video.

### 7. Lock it for reuse

Make the three-panel character sheet from [../styles/reference-sheets.md](../styles/reference-sheets.md), then hide the face in the front full-body panel so the close-up is the only detailed face. Pass sheet + identity still in every later shot.

### 8. Make it move

Motion block for any video of the avatar:
```
Every character keeps moving naturally: breathing, natural blinking, small shifts of weight, small hand gestures and hair moving slightly. No frozen poses and no slow motion unless the shot asks for it. Real unretouched skin and hands with five fingers.
```
Hold mode (the still is the moment): 3 to 4 micro-actions (blink, breath, hair drift, glance), "stays seated; does not stand" [tested].

Macro proof shots (skin, eye, sweat) sell realism in a sequence. Templates in realism.md under "Macro proof".

### Filled example (invented person, still)

```
Photorealistic medium close-up of a woman of about 34, a night-shift ER nurse, slim build, with faint freckles across her nose, a little shine on her forehead and tired shadows under her eyes, dark brown hair pulled back with a few loose strands across her cheek, and dark brown eyes. She wears navy scrubs with a faded ID lanyard. She holds a paper cup of coffee in both hands in a hospital break room at 6 a.m. The camera is at eye level, about one meter away, on an 85 mm lens at f/1.4: the focus is on her eyes, and her ears are already slightly soft. One flickering fluorescent tube above a vending machine to her left lights her face in cool-white light, about 4000 Kelvin; the rest of the room falls into soft gray shadow. No other light sources and no flat fill light. She gives a small, tired half smile because her shift just ended. Real, unretouched photographic skin: natural color variation across the face, a little shine on the forehead and nose, softer texture on the outer cheeks, normal creases under the eyes and real texture on the lips. Hair separates into uneven strands with a few flyaways, and makeup and clothing look lived in. A natural, in-the-moment expression rather than a posed model look. It reads as a frame from a film, not a stock photo or a beauty ad. No skin smoothing, waxy skin, porcelain teeth, glowing irises, uniform pore texture or helmet-like hair. No readable text, signs or logos.
```

## Pitfalls → fixes

| Pitfall | Fix |
|---|---|
| Waxy, airbrushed skin | Delete "flawless", "perfect", "8K", "hyper-realistic"; add the realism block; name 2 to 3 real skin details |
| Pores look like a pattern | Pores only in close-ups; "no uniform pore texture" on wider shots |
| Glowing or glassy eyes | "no glowing irises", one source = one catchlight, a little redness in the white |
| Flat light from everywhere | One source, side, color, how dark the room is, "no other light sources" |
| Sweat looks like oil or glitter | One bead or a light sheen in one place, with a cause, running downward |
| Twin does not look like the user | Face-lock line, faces first in the reference list, fewer style words, "Do not beautify or restyle the face" |
| Model looks like a stock-photo model | Write a person with a job and a week; give the expression a reason |
| Face changes between shots | Character sheet + identity still as references; trait line word for word; always i2i from the original still |
| Extra or melted fingers | Hands do one simple thing; "hands with five fingers"; regenerate only that shot |
| Black outfit vanishes into a dark set | One mid-tone outfit color [tested] |
| People freeze and stare in video | Motion block + one small physical action per shot |

<!-- Sources: prompt-styles realism.md, light-direction.md, aperture.md, reference-sheets.md (PromptWise free guides, fetched 2026-10-20); cinematic-story-reel references/prompt-guide.md sections 2 and 4 (identity still and hold mode, tested in an internal test reel); thumbnail SKILL.md face-lock line (adapted from higgsfield-youtube-thumbnail, MIT). -->
