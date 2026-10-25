# Light direction and hardness

Source: "AI Cinematic Lighting" (promptwise-free /15).

Two independent choices:
- **Direction**: front, side, back (relative to camera and subject). "Camera-left" = left as seen from the camera.
- **Quality**: hard (crisp shadow edges) or soft (gradual transitions). Any direction can be hard or soft.

Use one lighting block at a time. Replace any old lighting description with it.

## Lighting blocks

| Setup | Use for | Block |
|---|---|---|
| Soft front | presenter, beauty, clear face | A broad, diffused light near the camera evenly illuminates the front of the subject. Gentle shadows preserve shape, while bright areas retain detail. |
| Soft side | facial shape, product texture, beauty, interviews | A large diffused light close to the subject at camera-left makes the side nearest the light brighter, while the opposite side stays shaded. Shadows transition gradually, while the shaded side retains detail. |
| Soft back (rim) | outline against dark background | A soft light behind the subject, outside the frame, defines its outline against a darker background. A little soft light from the camera side keeps the front visible. |
| Hard side | bold fashion shadows, fabric texture | A small, undiffused light from camera-left creates crisp, clearly defined shadow edges. Side lighting brings out surface texture while highlights and shadows retain detail. |
| Hard front | (build it) | Describe a small source near the camera and crisp shadow edges. |

Silhouette is a separate choice: subject dark against a brighter background.

## What makes light hard or soft

Apparent size of the source from the subject. Larger = softer. Moving a broad source closer softens it; brightness does not. Direct sun = hard; overcast sky = broad soft source.

## Scene template

```
[Shot type] of [subject] in [setting], [one action]. [Camera movement]. [Lighting block]. [Visual style]. [Sound if needed].
```

Example: Medium close-up of a man in a charcoal jacket seated against a matte gray wall. He looks toward the camera and gives a small, relaxed smile. Consistent framing with subtle handheld movement. [Lighting block]. Photorealistic live action, natural skin texture, neutral color.

Image-to-video: put the lighting in the starting image, then describe only motion.

## One-light rule (from the Realism guide)

Decide four things before writing light:
- **Source**: a real object in the scene (desk lamp, window, candle, streetlight, phone screen).
- **Direction**: left, above, below, behind.
- **Color**: warm amber (bulbs, candles), neutral (daylight window), cold blue (screens).
- **Falloff**: how dark the rest of the room is, which side of the face goes to shadow.

```
One [light source] [where it sits] lights [the person]'s face in [warm amber] light from [the left]. The rest of the [room] falls into deep [green-gray] shadow, [with a little haze in the beam]. No other light sources and no flat fill light.
```

| Source | What it does to a face |
|---|---|
| Desk lamp / bare bulb | Warm hard light, fast falloff, face glows, room goes dark |
| Window by day | Soft neutral side light, gentle shadow on far cheek |
| Candle / fire | Very warm, low, flickering, lights from below |
| Phone / laptop screen | Cool blue from front-below, rest of head dark |
| Streetlight | Hard orange or white from above, deep shadows under brow |

Catchlight check: one lamp = one small reflection per eye. Rings, several, or none = the light in the prompt is unclear.

## Fixes

- **Unclear light**: replace "cinematic lighting" with a source, its position and the shadows you want.
- **Conflicting instructions**: remove lines that disagree on the same light (sharp AND gradual edges). One main light.
- **Soft light confused with blur**: ask for gradual shadow transitions AND sharp subject detail. Control focus separately.
- **Controlled comparison**: keep subject, action, background, framing, style identical; change only the lighting block. Check shadow edge first, then texture.
- **Before keeping a take**: light from the intended side? Shadow edges match? Subject readable while moving?
