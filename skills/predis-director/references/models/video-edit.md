# Clip editing and motion transfer (`runway_aleph_2`, `wan_2_7_videoedit`, `dreamactor_m2`)

**Predis options:**
- `runway_aleph_2`: no options; refs = 1 video (source) + up to 4 images; chooses own length. 27 cr/s.
- `wan_2_7_videoedit`: 720p|1080p, `duration` 2-10, aspect auto|16:9|9:16|1:1|4:3|3:4; refs = 1
  video + 1 image. 8 cr/s.
- `dreamactor_m2`: no options; needs 1 image (character) + 1 video (driving motion); chooses own
  length. 4 cr/s.

**Use for:** restyle, relight, weather/time change, add/remove/replace an object, wardrobe swap
(Aleph final, Wan videoedit to test); a still character performing a driving video (DreamActor).

## Compile (edit models)

The clip already carries composition, motion and timing. The prompt names **one change** with an
action verb (add, remove, replace, restyle, relight), then a keep line. 10 to 40 words.

```
Video 1 is the source. [Verb] [exact target] [to what]. Keep the framing, people, motion and
timing the same.
```

- With a style image: "image 1 sets colour palette and texture only; people and layout come from
  the video."
- One layer per pass (look, then weather, then object). Stack passes.
- Framing changes ("focus on the hand") fail from text; give a still of the target framing as the
  image ref.
- Prep: trim and downscale (`ffmpeg -i in.mp4 -t 10 -vf "scale=-2:720" prep.mp4`), strip audio if
  new sound is wanted.

## Compile (DreamActor)

Prompt, if any: identity locks only ("keep the character's face, outfit and colours exactly as the
image"). The work is in the inputs: one performer, steady camera, clean silhouette; character image
framed like the driver (both full length or both waist up), plain background. Use owned or licensed
driving footage.

## Good vs bad
Bad: `Make the video better, more cinematic and moody with rain and also anime style and a cat.`
Good: `Video 1 is the source. Relight the scene as late night with wet sodium-orange streetlight
from frame right. Keep the framing, people, motion and timing the same.`

## Failure modes
| Symptom | Fix |
|---|---|
| Unintended changes | shorter prompt, one change, keep line |
| Framing ignored | image ref of the target frame |
| Transfer has two people / noise | single-performer driver, matching framing |

## Self-check
- [ ] Exactly one change + a keep line
- [ ] Source trimmed to the model's limit

Sources: Runway Help Center Aleph article (via summaries), Runware Aleph 2.0 editing guide,
DataCamp Aleph test, predis-prompting/references/video-restyle.md.
