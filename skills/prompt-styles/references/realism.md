# Realism: skin, eyes, sweat, motion, consistent scenes

Source: "The AI Realism Playbook" (promptwise-free /17).

AI people look fake for the same reasons: airbrushed skin, light from nowhere, glowing eyes, nobody moves like a body. Ask for small physical evidence instead: visible pores, a pupil shrinking in bright light, a bead of sweat with a cause, a shadow falling away from the only lamp.

Workflow: (1) make each person and the empty location as separate stills; (2) zoom in on skin, eyes, hands; a waxy still stays waxy in video; (3) attach stills as references and use video prompts for motion, sweat, sound.

## Real skin, not "hyper-realism"

"Hyper-realistic, 8K, ultra detailed, flawless skin, perfect lighting, masterpiece" pushes toward over-sharpened retouched beauty-ad skin.

BETTER: Photorealistic close-up of a woman of about 30 sitting by a kitchen window on a gray morning, holding a mug of coffee and looking just past the camera with a half smile. Shot on an 85 mm lens at eye level, about a meter from her face. Soft daylight from the window on her left, the right side of her face falling into gentle shadow. Real, unretouched skin with faint freckles across her nose, a little shine on her forehead, fine lines at the corners of her eyes as she smiles and a few loose strands of hair across her cheek. No readable text.

## Realism block (paste at the end of any image prompt with a person)

```
Real, unretouched photographic skin: natural color variation across the face, a little shine on the forehead and nose, softer texture on the outer cheeks, normal creases under the eyes and real texture on the lips. Hair separates into uneven strands with a few flyaways, and makeup and clothing look lived in. A natural, in-the-moment expression rather than a posed model look. It reads as a frame from a film, not a stock photo or a beauty ad. No skin smoothing, waxy skin, porcelain teeth, glowing irises, uniform pore texture or helmet-like hair.
```

Match detail to distance: pores only in close-ups/macro. In medium/wide shots, asking for pores lays fake texture over the face.

## Light

Use one light with a reason to be there. See [light-direction.md](light-direction.md) for the one-light block, source table and catchlight check.

## Write a person, not a model

A specific person looks more real than a beautiful one. Give every detail a reason (age, job, their week).

```
Photorealistic [shot size] of a [woman or man] of [age], [what they do], [build], with [skin details], [hair] and [eyes]. [They] wear [clothing, with one sign of wear]. [They] [one simple action] in [location, time of day]. The camera is at [eye level], about [distance] away, framing [them] from the [waist] up on a [50 mm] lens. [One light source] lights [their] face from [direction], with [shadow] around [them]. [Their expression, and why].
```

Add the realism block after it. Keep signs, labels and logos out of frame. Give secondary characters a small habit (chewing gum, folded arms) to animate later.

## Macro proof (video)

Close-ups do most of the convincing. One detail per macro shot, lit by the same lamp, one small thing moves. Side or slightly-behind light shows pores and peach fuzz.

**Skin**
```
Extreme close-up of [a woman]'s cheek seen through a large round magnifying glass, shot on a 100 mm macro lens, one continuous shot. Her skin fills the frame in the warm light of [a hot desk lamp] from the side: every pore, fine peach fuzz catching the light and a few tiny freckles, sharp and real. The magnifying glass drifts slowly across her cheek, and the curved edge of the glass bends the image slightly. She breathes, and her skin moves very slightly. Real, unretouched skin. Sound: the low buzz of the lamp. No music, no text.
```

**Eye**
```
Extreme close-up of [a woman]'s [dark brown] eye on a 100 mm macro lens, one continuous shot. [A hot desk lamp] swings toward her face, and her pupil shrinks as the iris closes down in the bright light. Her lashes flicker, her lower lid tightens in a small squint, and a thin red vein shows in the white of her eye. One small reflection of the lamp sits in her eye, with a natural wet shine along the lower lid and real skin texture on the eyelid. No glowing iris. Sound: the buzz of the lamp. No music, no text.
```

**Sweat**
```
Extreme close-up on a 100 mm macro lens of [a woman]'s temple at her hairline, one continuous shot. In the heat of [the hot desk lamp], a single small bead of sweat forms on her skin, grows for a moment and then runs slowly down her temple, leaving a faint wet trail. The bead catches one bright highlight from the lamp. Fine hairs at the hairline, real pores and a little shine on the skin around it. The camera holds steady. Sound: the buzz of the lamp and a clock ticking. No music, no text.
```

## Small details need a reason

| Detail | Reason |
|---|---|
| Sweat at hairline or upper lip | Heat, hot light, a run, nerves |
| Flushed cheeks, pink nose tip | Cold wind, crying, a drink |
| Bloodshot eyes, shadows under | Long night, double shift, crying |
| Damp hair on forehead | Rain, workout, hot kitchen |
| Visible breath, goosebumps | Cold air |
| Creased shirt, loosened tie | End of a long day |
| Chipped polish, ink on fingers | Daily work and habits |

Pick two or three. "Sweaty glistening wet skin, dripping, glossy" coats the face in plastic shine; instead "A light sheen of sweat sits at his hairline and on his upper lip... just after a run".

## Motion block (video)

```
Every character keeps moving naturally: breathing, natural blinking, small shifts of weight, small hand gestures and hair moving slightly. No frozen poses and no slow motion unless the shot asks for it. Real unretouched skin and hands with five fingers.
```

- One action + reaction per 2-3 s shot; split longer moments.
- Physical reactions: squinting into light, swallowing when nervous, shivering.
- SOUND line with small real noises (lamp buzz, clock, chair creak) + "No music" for a recorded feel.

## One consistent multi-shot scene

1. Make the empty set (no people).
2. Make one still per character in the same light.
3. Attach in fixed order; keep CAST and LIGHT lines word for word.

Empty set image:
```
Photorealistic wide shot of [location] at [time of day], with no people in the frame. [Three or four key objects and their materials, with signs of wear]. The camera is at eye level about [three meters] away on a 35 mm lens, with [the main object] in the center of the frame. [One light source] throws [warm amber] light on [where it lands], while the rest of the [room] falls into deep [color] shadow, [with a little haze in the beam]. Real production design with believable materials and wear, no readable text, signs or logos anywhere.
```

Scene template:
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

- Names in CAPITALS, used identically in every line. If the tool uses @image1 tags, use them in REFERENCES.
- Too long for one take: split the shot list, restart timings at 0.0, keep REFERENCES/SET/LIGHT/CAST identical.
- Reference example in the guide: a 10-shot, ~28 s interrogation scene (detective + suspect, one tungsten desk lamp, green-gray tiles, macro skin/eye/sweat shots).

## Fix the tells

| Problem | Change |
|---|---|
| Waxy/airbrushed skin | Delete flawless/perfect/8K; add realism block; name 2-3 real skin details |
| Pores look like a pattern | Pores only in close-ups; "no uniform pore texture" on wider shots |
| Eyes glow/glassy | "no glowing irises", one source = one catchlight, a little redness in the white |
| Flat light from everywhere | One source, side, color; how dark the room is; "no other light sources" |
| Sweat like oil/glitter | One bead or a light sheen in one place, with a cause, running downward |
| Face changes between shots | Checked stills as references, fixed names, same CAST line |
| Light color changes | "LIGHT, identical in every shot" + same palette/contrast/exposure line |
| People freeze/stare | Motion block + one small physical action per shot |
| Extra/melted fingers | Hands do one simple thing, "hands with five fingers", regenerate that shot only |
| Gibberish text | "no readable text, signs or logos anywhere", paperwork closed or face down |
