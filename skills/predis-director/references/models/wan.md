# Wan (`wan_2_7`, `wan_2_5_i2v`, `wan_2_2_i2v_fast`)

**Predis options:**
- `wan_2_7`: 720p|1080p (default 1080p), `duration` 2-15, aspect 16:9|9:16|1:1|4:3|3:4. first +
  last frame. 12 cr/s. No audio switch.
- `wan_2_5_i2v`: needs an image. 480p|720p|1080p, `duration` 5|10. first_frame + **1 audio ref**
  (voice or music drives the motion/mouth). 8 cr/s (5 s 41).
- `wan_2_2_i2v_fast`: 480p|720p, `duration` 5-10, aspect 16:9|9:16|1:1. first frame. 2 cr/s (5 s 9).
  Despite the id it also does t2v.

**Use for:** cheapest motion drafts (2.2 fast), lip-sync to a voice file you already have (2.5
with audio ref), mid-price clean single shots and short 2 s inserts (2.7).
**Not for:** multi-character acting, multi-shot.

## Compile

Text to video (Alibaba formula): **Subject + Scene + Motion + Aesthetic control (light, lens,
camera, time of day) + Stylization**. Image to video: **Motion + Camera movement** only.
Length: 30 to 120 words, literal; very long prompts distort.

```
t2v: [Subject trait line] in [scene]. [Motion with endpoint]. [Light], [lens], camera [one move]. [Style].
i2v: [Motion with endpoint]. Camera [one move]. [One ambient motion]. Keep [face/product] unchanged.
```

- With an audio ref (2.5): "The man in the image speaks to camera in time with the audio,
  natural head movement, steady medium close-up." Keep the face large in frame.
- If it morphs or cuts: "single continuous shot" and one action.

## Good vs bad
Bad: a 250-word paragraph with five actions and three camera moves.
Good (i2v draft): `The boxer tips backward and lands flat on the canvas in slow motion. Camera
static, wide. Dust lifts from the mat. Keep both faces and outfits unchanged.`

## Failure modes

| Symptom | Fix |
|---|---|
| Distortion on long prompts | cut to <= 120 words, one action |
| Lip-sync drifts | shorter audio, bigger face, calm camera |
| Same take every time | vary the wording |

## Self-check
- [ ] Formula order respected (t2v) or motion+camera only (i2v)
- [ ] `wan_2_5_i2v` has an image; audio ref if lip-sync
- [ ] Duration valid (2.5: 5|10)

Sources: Alibaba Cloud "Model Studio Wan video generation prompts recipe" (formulas), Morphic
Wan 2.7 page.
