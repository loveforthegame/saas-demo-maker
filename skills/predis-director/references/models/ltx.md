# LTX (`ltx_2_5_pro`, `ltx_2_5_fast`, `ltx_2_3_pro`, `ltx_2_3_fast`)

**Predis options:** all have `aspect` 16:9|9:16, `audio` (default true), first + last frame.
- `ltx_2_5_pro`: 720p|1080p, `duration` 6|8|10. 14 cr/s.
- `ltx_2_5_fast`: 720p-4K, `duration` 6-20 (even). 11 cr/s.
- `ltx_2_3_pro`: 1080p|1440p|4K, `duration` 6|8|10. 5 cr/s (6 s 29).
- `ltx_2_3_fast`: 1080p-4K, `duration` 6-20 (even). 3 cr/s.

**Use for:** long single takes up to 20 s cheaply, high-res (1440p/4K) output, controlled A-to-B
with first + last frame at low cost, macro and atmosphere.
**Not for:** hard cuts inside one clip, 1:1 or 4:5, under 6 s.

## Compile

Write **one flowing paragraph, present tense, 4 to 8 sentences, chronological**. No line breaks,
no lists, no labels. Order: **shot framing -> scene -> action unfolding -> character -> camera
movement -> audio**. Chain beats with "as", "then", "while".

```
[Shot framing and lens]. [Scene and light]. [Subject trait line] [first action], then [second
action] as [environment reacts]. The camera [move, speed] until [describe what the frame shows
when the move ends]. [Audio: ambient, effects, dialogue in quotes].
```

- Detail scales with shot size: close-ups need more texture and micro-movement; wides need less.
- Emotion as physical cues ("her eyebrows lift slightly"), not labels.
- State where the camera ends up: LTX finishes moves better when it knows the end framing.
- i2v: describe the source image briefly and build on it, then the motion.
- A short closing "avoid flicker" style clause is tolerated; keep it to one clause.

## Good vs bad

Bad (labels, fragments):
> Shot 1: boxer. Shot 2: falls. Camera: zoom. Style: cinematic, 4K.

Good:
> A wide low-angle shot from the ring corner on a 24mm lens. Warm tungsten beams cut through dust
> above a worn blue canvas. The giant bearded boxer in red satin shorts tips backward from his
> heels, then sails through the air in slow motion as sweat drops spray into the light, while the
> small boy in blue gloves stays frozen with his glove out. The camera holds still until the boxer
> lies flat on his back and a puff of dust settles around him. Muffled crowd gasps fill the gym.

## Failure modes

| Symptom | Fix |
|---|---|
| Move never completes | describe the end framing after the move |
| Rewritten into something else | the host may run a prompt rewriter; be concrete, not poetic |
| Unwanted cut | it is a one-take model; remove any "shot" labels |

## Self-check
- [ ] Single paragraph, present tense, 4-8 sentences
- [ ] Ends-of-move described
- [ ] Duration is an allowed value (>= 6)

Sources: Lightricks "Prompting Guide for LTX-2" (docs.ltx.video, via search summary), RunDiffusion
LTX-2 guide.
