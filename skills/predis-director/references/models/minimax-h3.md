# MiniMax H3 (`minimax_h3_max`, `minimax_hailuo_3`)

**Predis options:**
- `minimax_h3_max`: `resolution` 480p|768p (default 768p), `duration` int 5-15, aspect
  1:1|16:9|9:16|4:3|3:4. first + last frame. No audio switch. 7 cr/s (5 s 33). ~35 s per run.
- `minimax_hailuo_3`: `duration` 5-15, same aspects. Ref modes: `references` (9 images, 3 videos,
  3 audio) or `keyframes`. 11 cr/s. Also v2v.

**Use for:** one-beat acting shots (a breath, a smirk, a wink), performance with body language,
fast cheap retakes, audio-ref driven mouth rhythm (`hailuo_3`).
**Not for:** impacts and contact physics, liquids, crowds by count, on-screen text, many beats per shot.

## Compile

Decide in this order: **purpose (feeling) -> framing -> content**. Then write:
**framing in one line -> subject -> body-first performance with timed beats -> light**. 40 to 120
words. Describe what is in the frame in detail; how it is shot in one line.

```
[Shot size], [camera height], [static on a tripod | one move]. [Subject trait line, as visible].
At 0-1.5s [body beat]. At 1.5-3s [the one face beat, written as muscle order]. Between beats he
breathes, blinks, weight settles. [Light sources]. [look_line].
```

- One shot holds 1 to 2 expression beats. More: split into shots.
- Write emotions as body order, not labels: "lower lids push up first, then the mouth corners
  lift" (real smile), never "he smiles warmly".
- Stillness: objects as positive states; people as small living actions; camera in ONE sentence.
  Never "nothing changes" or a list of "no zoom, no push-in".
- Size: crop language ("the top of his head is one hand's width below the frame edge"), not
  fractions or units.
- Face beats need the face >= 1/3 of frame height.
- Impacts: skip the contact moment; show before and after, put the hit in the sound/edit.
- Optional camera commands (Hailuo legacy syntax, may help): `[Push in]`, `[Static shot]`,
  `[Tracking shot]`, max 3 in one bracket. Prose must still state the move.
- Leave ~1.5 s tail; final second can break.

## Good vs bad

Bad (adjectives, many beats, "nothing moves"):
> The boxer looks down amused, smirks, laughs, then gets serious, then winks. Nothing else moves,
> no zoom, no pan, no push-in.

Good (first frame = B3):
> Close-up, camera slightly below his chin, static on a tripod. The giant boxer with the thick
> black beard looks down at the boy below frame. At 0.5s his head tilts a few degrees down. At
> 1.2s his lower lids push up first, then one corner of his mouth lifts into a slow smirk that
> holds. Between beats he breathes and blinks; sweat beads on his forehead catch the ring lights.
> Warm tungsten backlight.

## Failure modes

| Symptom | Fix |
|---|---|
| Frozen face | too many beats; one beat per shot, fill time with countable small events |
| Face morphs like rubber | hide the change behind a blink or head dip; counter-beat first |
| Character looks into the lens | move the camera to where they look; "does not look into the lens" |
| Hand-object contact fails | make the moving body part the subject; contact from frame 1 |
| Crowd count wrong | set it in the scene image, not text |
| Cut lands late | tie it to an event, not a timestamp |

## Self-check
- [ ] Intent -> framing chosen on purpose (not centered eye-level by default)
- [ ] <= 2 expression beats; emotions written as body order
- [ ] Camera in one sentence; no "nothing changes"
- [ ] No impact or liquid volume on screen

Sources: predis-prompting/references/minimax-h3.md (production diary, deep notes: read on a
second failure), Akool Hailuo guide (failure modes), Hailuo bracket camera commands (third-party).
