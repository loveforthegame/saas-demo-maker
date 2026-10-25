# Other image models (`qwen_image_3`, `mai_image_2_5`, `grok_imagine_image_2`, `krea_2_turbo`, `p_image`)

**Predis options:**
- `qwen_image_3`: t2i, `resolution` 1K|2K, aspect 16:9|9:16|1:1|4:3|3:4. 3 cr. Slow (~275 s).
- `mai_image_2_5`: t2i, aspect 1:1|4:3|3:4|16:9|9:16|3:2|2:3. 4 cr.
- `grok_imagine_image_2`: t2i + i2i, `resolution` 1K|2K, `quality` low|medium, 13 aspects incl.
  9:19.5; up to 3 refs. 5 cr.
- `krea_2_turbo`: t2i, 1K|2K, 5 aspects. 0.64 cr. `p_image`: t2i, 7 aspects. 0.41 cr.

**Use for:** an alternative look when the main models feel samey (MAI, Qwen), stylized bold
stills (Grok), near-free drafts and moodboards (Krea, p-image).

## Compile

No model-specific official guides found (2026-10-15). Use the universal image grammar:
**subject -> action -> setting -> composition -> light -> style**, full sentences, 30 to 80 words,
positive phrasing only. Drafts: 15 to 40 words, composition and light only; no text, no refs.

```
[Subject] [action] in [setting]. [Shot size, angle]. [Light source]. [Style medium].
```

## Good vs bad
Bad: `boxer kid gym, 8k, trending`
Good (draft): `Wide low angle: a giant boxer faces a tiny boy in a boxing ring, kids at the ropes, warm
overhead light, film still.`

## Failure modes
| Symptom | Fix |
|---|---|
| Text garbled on drafts | drafts never carry text |
| Grok edit looks soft | `quality` medium; refs <= 3 |

## Self-check
- [ ] Drafts used only to pick composition; final on a router default

Sources: describe_model only. Log learnings here after real runs.
