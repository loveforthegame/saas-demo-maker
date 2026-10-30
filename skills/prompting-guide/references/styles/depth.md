# Depth: foreground, midground, background

Source: "AI Depth Hack" (promptwise-free /2).

Depth is more than blur. Distance, overlap and perspective make space readable even with a recognizable background. Two clear depth regions can be enough.

- **Foreground**: closest to the camera. A nearby object overlapping part of the frame shows what sits in front of what.
- **Midground**: the subject.
- **Background**: farthest visible part.

Keep the face and the important action unobstructed.

## Prompt blocks (pick what the shot needs)

| Block | Contents |
|---|---|
| Subject and setting | who/what, where |
| Framing | shot size, camera height, viewing direction |
| Placement | what is near the lens, where the subject sits, what extends behind |
| Light and visibility | source and direction, focus, details that must stay readable |
| Atmosphere (optional) | haze/mist/particles in a *specified* part of the scene |

## Starting frame template (IMAGE)

```
Photorealistic [shot size] of [subject] in [location]. The camera is at [height], looking [direction]. [Foreground element] sits close to the lens and frames [edge]. The subject is [position] beyond it. [Background] extends farther behind. [Light source] illuminates the subject from [direction]. Focus on [important detail], while keeping [background detail] recognizable.
```

Be specific. Not "a plant in the foreground" but "A few leaves close to the lens frame the lower-left corner. The person stands several steps beyond them, with their face unobstructed."

## Animate template (VIDEO, image-to-video)

```
Animate @image1. The camera [one clear movement] with subtle handheld motion, keeping [subject] framed. The subject [one simple action]. [Existing atmospheric element] moves [direction and speed]. Preserve the setting and light direction.
```

- The image already carries look, light, composition. The video prompt only adds camera motion, action, movement in the existing environment.
- `@image1` is one tag style. If the model uses a first-frame slot instead of tags, load the image there and drop "Animate @image1." Tag syntax per model: `../models/<family>.md`.
- Text-to-video: combine the IMAGE description with the VIDEO instructions, drop the reference sentence.
- Parallax line that sells depth: "the nearby doorframe shifts more than the distant shelves."

## Localized atmosphere lines

Name type, location, density; for video also how it moves and what stays visible. Never cover the whole frame.

| Air | Line |
|---|---|
| Haze (distant landscape) | A thin atmospheric veil sits over the distant hills. Contrast decreases with distance, while the nearby subject remains clear and detailed. |
| Mist (water, damp morning) | Thin patches of mist hover above the distant river behind the subject. They drift slowly sideways in a light breeze. The foreground remains clear. |
| Low-lying fog | Low-lying fog drifts gently through the hollow behind the subject, below knee height. Their face and upper body remain unobstructed. |
| Dust (dry ground) | A thin dust trail follows the vehicle over dry ground. A light crosswind carries it sideways. The vehicle remains clearly visible. |
| Smoke | A thin smoke plume rises from a distant chimney and bends gently with the wind. The subject stands in clear air closer to the camera. |
| Steam | A fine wisp of steam rises above the hot cup, visible against the darker background. The surrounding room remains clear. |

Terms: mist and fog are water droplets; haze is fine dry particles; heat shimmer is optical distortion, not haze. A visible beam needs a light path plus particles: "Directional sunlight enters through a high rear window, revealing sparse dust in the beam."

## Example pattern (doorway portrait)

IMAGE: Photorealistic medium shot of a woman in a small ceramics studio. The camera looks in from just outside the entrance, slightly below eye level. A wooden doorframe close to the lens occupies the left edge. She stands several steps beyond it. Pottery shelves extend farther behind her. Soft window light enters from the right. Her face is in focus; the studio remains recognizable.

VIDEO: Animate @image1. In one continuous shot, the woman turns her head slightly toward the window. The camera moves a little to the right with subtle handheld motion, keeping her framed. In the image, the nearby doorframe shifts more than the distant shelves. Preserve the setting and light direction.

Variants: over-the-shoulder reaction (foreground shoulder belongs to the person they look at), reeds framing a riverside portrait with mist only in the distance, product with a dish edge in the lower-left corner and "clear air".

## Fixes

| Problem | Write |
|---|---|
| Foreground covers the action | "The foreground leaves remain in the lower-left corner. The subject's face and working hands stay unobstructed." |
| Background detail disappears | "Keep the person in focus while retaining recognizable shapes and visible activity in the background." |
| Placement unclear | "The subject stands several steps beyond the doorway. The rear wall is farther behind them." |
| Mist covers the whole scene | "Thin mist remains above the distant water, behind the subject. The foreground and subject stay clear." |
| Pan instead of sideways move | "The camera physically moves sideways to the right, keeping the subject framed." (A pan rotates in place.) |

## WEAK → BETTER

WEAK: A woman in a ceramics studio, cinematic depth, blurry background, atmospheric.

BETTER: Photorealistic medium shot of a woman in a small ceramics studio. The camera looks in from just outside the entrance, slightly below eye level. A wooden doorframe close to the lens occupies the left edge. She stands several steps beyond it. Pottery shelves extend farther behind her. Soft window light enters from the right. Her face is in focus; the studio remains recognizable.

## Where it fails

- A foreground object placed vaguely ("a plant in the foreground") lands anywhere, often over the face or the action.
- Air written for "the scene" fills the whole frame; pin it to one region.
- A pan rotates in place and gives no parallax; depth needs the camera to physically move sideways.
- Blur alone is not depth. Without overlap and distance, a blurred background still reads flat.

<!-- Source: prompt-styles/references/depth.md, distilled from PromptWise "AI Depth Hack" (promptwise-free.vercel.app/2), fetched 2026-10-20. -->
