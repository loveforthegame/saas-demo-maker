# Seedance 1.x (`seedance_1_5_pro`, `seedance_1_pro`, `seedance_1_lite`)

**Predis options:**
- `seedance_1_5_pro`: `resolution` 480p|720p|1080p, `duration` 4-12 + auto, aspect 1:1|16:9|9:16|4:3|3:4,
  `audio` (default false). first + last frame. 2 cr/s (5 s 11).
- `seedance_1_pro`: resolution up to 1080p, `duration` 2-12, same aspects. first + last. 4 cr/s.
- `seedance_1_lite`: 480p|720p, `duration` 2-12. first frame only. 3 cr/s.

**Use for:** cheap single-take shots, short inserts (2 s minimum on 1_pro / 1_lite), motion drafts,
people shots when Seedance 2 refuses face refs.
**Not for:** multi-shot, multi-reference, dialogue.

## Compile

Order: **subject + action -> scene -> camera -> light/style**. 30 to 80 words. One action, one move.

```
[Subject or "the [role] in the image"] [action with endpoint]. Camera: [one move]. [Light]. [look_line].
```

- i2v: motion + camera + preserve line only.
- No tags, no shot labels. Add "single continuous shot" if it cuts.

## Good vs bad
Bad: `Shot 1: ... Shot 2: ... @Image1 ...` (features it does not have)
Good: `The boy in the image grins wide, showing his missing front tooth, and raises his blue glove.
Camera: slow push-in from medium to close-up. Warm tungsten light. 35mm film.`

## Failure modes

| Symptom | Fix |
|---|---|
| Mushy action | one verb with a visible endpoint |
| Unwanted cut | "single continuous shot" |

## Self-check
- [ ] One action, one move, <= 80 words
- [ ] Duration within the model's min (2 or 4)

Sources: describe_model; predis-prompting/references/seedance.md.
