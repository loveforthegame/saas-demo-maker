# Nano Banana (`nano_banana_pro`, `nano_banana_2`, `nano_banana_2_1`)

**Predis options:** `resolution` 1K|2K|4K (Pro default 2K, others 1K); `aspect` 1:1|4:5|16:9|9:16
(2.1 adds 5:4, 4:3, 3:4, 3:2, 2:3, 21:9, 9:21, 4:1, 1:4, 8:1, 1:8). Ref mode `references`: up to
**14 images**. Up to 4 outputs. 7 / 4 / 2 cr per image.

**Use for:** photoreal keyframes for video, character and set references, multi-ref composites
(put person 1 in outfit 2 in place 3), consistent edits, structured layouts via JSON.
**Not for:** long typeset copy (GPT Image / Ideogram).

## Compile

It reasons before rendering: write **natural-language sentences, never tag lists**.
Order: **intent/use -> subject (trait line) -> action/pose -> setting -> composition/camera ->
light -> style -> text -> constraints**. 50 to 150 words. Up front, say what the image is for
("first frame of a vertical video shot").

```
[Use: "Vertical 9:16 film still, first frame of a video shot."] [Ref roles: "Use the boxer from
image 1 and the boy from image 2, faces and outfits identical; the gym from image 3."]
[Subject + pose/action frozen at a stable moment]. [Composition: shot size, angle, where each
subject sits, what fills the foreground/background]. [Light sources]. [look_line].
```

- Refs: number by reference_ids order, one role each, and say what not to take from each.
- Keyframes for video: freeze a **stable, readable start state**, not mid-air action. The video
  model animates from it.
- Edits: "Change only X. Keep pose, expression, framing, light and everything else identical."
  Name what fills a removed area.
- Structured JSON (product hero, social graphic, UI mock, chart): lead line "Render this
  specification as one high-fidelity image." + valid JSON with stable keys. Only for defined targets.
- Quoted text renders well for short headlines; keep body copy out.

## Good vs bad

Bad:
> boxer, kid, gym, boxing, cinematic, 8k, ultra detailed, masterpiece

Good:
> Vertical 9:16 film still, the first frame of a video shot. Use the boxer from image 1 and the
> boy from image 2 with faces and outfits identical, inside the gym from image 3. Wide low-angle
> shot from a ring corner: the giant boxer stands in the centre of the ring facing the small boy,
> both with gloves up, the boy reaching only to the boxer's belt. Schoolkids in yellow t-shirts
> crowd the red ropes behind them. Warm tungsten overheads, dust in the beams. 35mm film, shallow
> depth of field, soft grain.

## Failure modes

| Symptom | Fix |
|---|---|
| Identity drifts across stills | same refs every time, re-anchor on the ORIGINAL ref, trait line verbatim |
| Two copies of a person | headcount line; one ref per person |
| Mid-action frame animates badly | regenerate as a stable start state |
| Angle change edit fails | new generation from refs instead of editing |

## Self-check
- [ ] Use/intent stated first; full sentences
- [ ] Refs numbered in reference_ids order with roles
- [ ] Keyframes are stable start states
- [ ] Aspect in config matches the video aspect

Sources: Google AI Studio Nano Banana Pro tips (natural language over tags, 14 refs; via
secondary reports), predis-prompting/references/image-models.md.
