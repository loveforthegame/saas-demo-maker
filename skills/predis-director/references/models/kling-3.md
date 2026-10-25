# Kling 3 (`kling_3_pro`, `kling_3_standard`)

**Predis options:** `duration` int 5-10 (default 5), `aspect` 16:9|9:16|1:1, `audio` bool
(default true). Ref mode `keyframes`: first_frame + last_frame. Image refs min 300 px, max aspect
2.5. No resolution option. Price at 5 s, 9:16: Pro 91 audio off / 137 on; Standard 68 / 102.

**Use for:** bodies with weight, contact, falls, stunts, lifts; controlled A-to-B arcs with a last
frame; dialogue scenes when Veo is not an option (native audio, multi-language).
**Not for:** shots under 5 s of real need (min 5), identity from several refs (use Kling O3).

## Compile

Order: **subject (trait line) -> action with cause and consequence -> setting -> camera -> light
-> style -> audio**. Length: 50 to 120 words for one shot; up to ~6 labelled shots in one clip.

```
[Subject trait line] [action, written as cause -> visible consequence -> endpoint]. [Setting].
Camera: [shot size], [one move from X to Y, speed]. Light: [sources]. Style: [look_line].
```

- Kling reads film language ("tracking shot", "profile shot", "macro close-up", "POV",
  "shot-reverse-shot"). Use it, one move per shot.
- Image to video: the first frame is the anchor. Write only motion, camera, change over time and
  what stays: "preserve faces, outfits and the ring; only ...". Do not re-describe the image.
- First + last frame: describe the transition only, and make the last frame the physical end
  state (seated, landed, closed).
- Multi-shot (no Predis storyboard field, prose works): a one-line master description of the
  subjects first, then `Shot 1 (0-4s): ...` `Shot 2 (4-8s): ...`, each with framing, subject,
  motion. Subject descriptions identical in every shot.
- Dialogue: label speakers with a bracketed, unique descriptor including voice:
  `[Black-suited agent, raspy deep voice]: "..."`. Put the physical action before the line. Use
  "Immediately," when the speaker switches. Never "he says".
- Audio off when sound comes in the edit: config `audio=false`, no sound words.

## Good vs bad

Bad (first frame re-described, two moves, no endpoint):
> A huge boxer with a beard and tattoos in a gym falls down dramatically, camera zooms and pans
> around, epic cinematic slow motion.

Good (i2v, first frame = boxer upright after the jab):
> The giant boxer throws himself backward from his heels, arms flung wide like a stage dive, sails
> through the air in slow motion with sweat drops spraying into the light, and lands flat on his
> back on the blue canvas, a puff of dust lifting off the mat. The small boy stays frozen with his
> blue glove still out. Camera: wide, static, low angle from the ring corner. Preserve both faces,
> outfits and the gym exactly.

## Failure modes

| Symptom | Fix |
|---|---|
| Camera wanders | one move with start and end, or "Camera: static, on a tripod" |
| Face drifts from the first frame | delete re-description; add "preserve faces and outfits" |
| Motion too timid | one bigger physical action with a visible result |
| Plug/lid/hand-object never meets | name the real parts, make start + end keyframes, use last_frame |
| Speakers merge | bracketed unique labels, action before line, "Immediately," at switches |
| Paying for audio you will replace | `audio=false` (one third cheaper) |

## Self-check
- [ ] Trait line verbatim (t2v) or a preserve line (i2v)
- [ ] Action written as cause -> consequence -> endpoint
- [ ] One camera line; duration 5-10; audio flag matches the brief
- [ ] Last frame given whenever the end state matters

Sources: fal.ai Kling 3.0 prompting guide; predis-prompting/references/kling.md.
