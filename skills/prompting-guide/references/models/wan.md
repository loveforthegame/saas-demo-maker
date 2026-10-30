# Wan (Wan 2.7, Wan 2.5 i2v, Wan 2.2 i2v Fast)

**Model facts (at the time of writing; confirm in your provider):**
- Wan 2.7: 720p or 1080p; 2 to 15 s; 16:9, 9:16, 1:1, 4:3, 3:4; first + last frame; no audio
  switch. Mid cost.
- Wan 2.5 i2v: needs an image. 480p to 1080p; 5 or 10 s; first frame + **one audio reference**
  (a voice or music file drives the motion and mouth). Mid-to-cheap.
- Wan 2.2 i2v Fast: 480p or 720p; 5 to 10 s; 16:9, 9:16, 1:1; first frame. Despite the name it
  also does text to video. Near-cheapest video option.
- Wan 2.7 video edit is a separate model: see video-edit-restyle.md.

Check the provider's model options for the exact parameter names (duration, aspect ratio, first/
last frame, audio reference slot).

## When to pick it

- **Use for:** cheapest motion drafts (2.2 Fast), lip-sync to a voice file you already have (2.5
  with an audio ref), avatar / talking-head clips from one portrait + a voice file (2.5),
  mid-price clean single shots, short 2 s inserts and long takes up to 15 s (2.7).
- **Not for:** multi-character acting, multi-shot.

## Compile

- **Slot order:**
  - Text to video (Alibaba formula): Subject + Scene + Motion + Aesthetic control (light, lens,
    camera, time of day) + Stylization.
  - Image to video: Motion + Camera movement only.
- **Length:** 30 to 120 words, literal. Very long prompts distort.
- **Timing:** none. One action, one move, one ambient detail.
- **References:** first frame (and last frame on 2.7). On 2.5 the audio file is the timing
  reference.
- **Audio:** with an audio ref (2.5): "The man in the image speaks to camera in time with the
  audio, natural head movement, steady medium close-up." Keep the face large in frame.
- **When a reference carries it:** with a first frame, describe the change, not the picture.
- If it morphs or cuts: add "single continuous shot" and cut to one action.

```
t2v: [Subject trait line] in [scene]. [Motion with endpoint]. [Light], [lens], camera [one move]. [Style].
i2v: [Motion with endpoint]. Camera [one move]. [One ambient motion]. Keep [face/product] unchanged.
```

### Example

Bad: a 250-word paragraph with five actions and three camera moves.
Good (image to video draft): `The boxer tips backward and lands flat on the canvas in slow
motion. Camera static, wide. Dust lifts from the mat. Keep both faces and outfits unchanged.`

## Self-check

- [ ] Formula order respected (text to video) or motion + camera only (image to video)
- [ ] Wan 2.5 has an image; audio ref if lip-sync
- [ ] Duration valid (2.5: 5 or 10 s)

## Failure modes

| Problem | Fix |
|---|---|
| Distortion on long prompts | cut to 120 words or fewer, one action |
| Unexpected cut or morph | "single continuous shot", one action |
| Lip-sync drifts | shorter audio, bigger face, calm camera |
| Same take every time | vary the wording |

## Field notes

### Cheap-draft workflow (Wan 2.2 i2v Fast, also LTX 2.3 Fast)

1. Lock the look as an image first (image model), then animate it.
2. Prompt only motion, camera and sound; the image carries style, grade and composition.
3. Run 2 or 3 takes of the draft, pick the motion that works, then re-run that prompt on a
   premium model.

Draft prompt shape:
`[one subject action with endpoint]. Camera: [one move]. [one ambient motion: steam, hair, leaves]. Keep [face/product/layout] unchanged.`

Check aspect ratios and maximum duration before promising vertical or long clips.

Sources: Alibaba Cloud "Model Studio Wan video generation prompts recipe" (formulas); Morphic
Wan 2.7 page; internal production field notes.
