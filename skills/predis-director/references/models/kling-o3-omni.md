# Kling O3 Pro and Kling 3 Omni (`kling_o3_pro`, `kling_3_omni`)

**Predis options:**
- `kling_o3_pro`: `duration` int 3-15 (default 5), `aspect` 16:9|9:16|1:1, `audio` bool (default
  true). Ref mode `combined`: first_frame (1) + reference images (up to 4). 9 cr/s audio off
  (3 s 27, 4 s 36, 5 s 46), 11 cr/s on.
- `kling_3_omni`: `mode` standard|pro, `duration` 3-15, `aspect` 16:9|9:16|1:1, `audio` (default
  false). Ref mode `references`: up to 7 images + 1 video. 14 cr/s. Also v2v (edit a clip with refs).
- Image refs min 300 px, max aspect 2.5.

**Use for:** the same character across many shots (first frame + identity refs in one call), short
shots (3 s minimum), reference-driven scenes, editing a clip while adding a referenced object.
**Not for:** heavy physics stunts (Kling 3 Pro), dialogue-led hero shots (Veo).

## Compile

Order: **reference roles -> action -> environment -> camera -> light -> style**. Length 40 to 100
words. Refer to references by their order in `reference_ids`: write "image 1", "image 2" and, for
safety across hosts, the tag form in brackets once: "the boxer (@Image2)". Keep the prose readable
without the tag.

```
Image 1 is the first frame. The [role] from image 2 and the [role] from image 3 keep their faces
and outfits exactly. [Action with endpoint]. Camera: [one move]. Light: [only changes]. [look_line].
```

- O3 is optimized for 1 to 2 identity references. Four refs is the ceiling, not the target.
- Give each ref one job (identity, outfit, product, set) and say what must not transfer
  ("only the face from image 2, not its background or pose").
- With a first frame, never re-describe it; describe what moves.
- Omni with a video ref: "Video 1 is the source; keep its timing and camera; change only ...".

## Good vs bad

Bad:
> Make a video with these images of the boxer and the kid in the gym doing boxing.

Good (first frame B2 + ref A2):
> Image 1 is the first frame. The boy from image 2 keeps his face, freckles and missing front
> tooth exactly. He draws one deep breath that lifts his small shoulders; the oversized blue
> headgear slides down over one eyebrow; he pushes it back up with his blue glove and frowns
> harder. Camera: close-up, static, slight handheld drift. 35mm film, warm tungsten, soft grain.

## Failure modes

| Symptom | Fix |
|---|---|
| Two copies of one person | state headcount: "exactly two people: the boxer and the boy"; fewer refs per person |
| Ref background leaks into the shot | "take only the face and outfit from image 2" |
| Wrong ref used for wrong role | reference_ids order must match the prompt numbering |
| Stiff motion | one bigger body action; 3-5 s is enough |

## Self-check
- [ ] First frame listed first in reference_ids, then refs in prompt order
- [ ] Each ref has one role + a "not" clause
- [ ] Duration chosen from used_s + 1.5 (3 s is allowed)
- [ ] Audio flag matches the brief

Sources: Kling blog "V3 vs O3" (1-2 elements optimal), Runware/Opper O3 docs (element syntax
varies by host), predis describe_model.
