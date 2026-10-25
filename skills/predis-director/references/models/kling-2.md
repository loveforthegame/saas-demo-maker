# Kling 2.x (`kling_2_6`, `kling_2_5_turbo`, `kling_2_1`)

**Predis options:**
- `kling_2_6`: `duration` 5|10, `aspect` 16:9|9:16|1:1, `audio` (default true). first_frame only. 11 cr/s.
- `kling_2_5_turbo`: `duration` 5|10, `aspect` 16:9|9:16|1:1. first_frame only. 6 cr/s (5 s 28).
- `kling_2_1`: i2v only, needs an image. `mode` standard|pro, `duration` 5|10. first + last frame. 4 cr/s.

**Use for:** cheap motion drafts of a Kling 3 shot (turbo), cheap animate-a-still with an end state
(`kling_2_1` first+last), aggressive camera moves (turbo follows "fast drone follow", "whip pan").
**Not for:** dialogue, multi-shot, identity across many refs.

## Compile

Order: **subject -> action -> camera -> environment -> style**. Length 30 to 80 words. Shorter than
Kling 3; one action, one move.

```
[Subject, 3-5 traits or "the [role] in the image"] [one action with endpoint]. Camera: [one move].
[Setting only if t2v]. [look_line].
```

- i2v: motion + camera + "preserve face and outfit"; nothing else.
- To promote a turbo draft to `kling_3_pro`, keep the prompt and add the full trait line and light.

## Good vs bad
Bad: `boxer falling, dramatic, slow motion, 8k, masterpiece`
Good: `The boxer in the image tips backward and falls flat onto the canvas in slow motion, arms
wide. Camera: static wide. Preserve his face, beard and red gloves.`

## Failure modes

| Symptom | Fix |
|---|---|
| Static output | stronger verb, a visible result, a speed word |
| Jitter or melting on 10 s | use 5 s; split the action |
| "static" in an avoid list kills camera motion | never write "no static"; state the move |

## Self-check
- [ ] <= 80 words, one action, one move
- [ ] Duration is 5 or 10 (enum)
- [ ] `kling_2_1` has an image ref

Sources: VEED and Artlist Kling 2.5 Turbo guides; Hedra model page.
