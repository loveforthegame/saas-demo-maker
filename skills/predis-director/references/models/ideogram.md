# Ideogram (`ideogram_v3_quality`, `ideogram_4_5`, `ideogram_4_5_precise_edit`)

**Predis options:**
- `ideogram_v3_quality`: aspect 15 ratios (incl. 9:16, 4:5, 3:1); **`style_type`** None|Auto|General|Realistic|Design;
  up to 3 style ref images (t2i). 7 cr.
- `ideogram_4_5`: `quality` low|medium|high; aspect auto|1:1|10:7|7:10|7:4|4:7|12:5|5:12 (no 9:16:
  use 4:7 and crop); up to 5 refs. 5 cr.
- `ideogram_4_5_precise_edit`: i2i only; `quality` very low..high; ref mode `edit` = 1 **source**
  + up to 4 refs. 5 cr.

**Use for:** typography-led images (logos, wordmarks, posters, stickers), fixing text inside an
existing image (precise edit).
**Not for:** photoreal keyframes for video.

## Compile

**Put the text near the start of the prompt, in quotes.** Then the design around it. 20 to 80
words. Shorter text = fewer errors.

```
[Format: poster | logo | sticker] with the text "[EXACT]" in [lettering style], [placement].
[Imagery]. [Palette]. [Layout/background].
```

- Never negative phrasing ("no people", "without trees"): describe what fills the space.
- v3: set `style_type` = Design for graphic layouts, Realistic for photo-like, rather than
  describing it in words.
- Precise edit: source first in reference_ids; "Change "OLD" to "NEW", keep font, colour and
  position." Keep new text close in length to the old.

## Good vs bad
Bad: `a poster without people, no clutter, write something about boxing`
Good: `Poster with the text "GO LEO!" in thick hand-painted brush letters, slightly uneven, centred
on torn brown cardboard, black marker outline, small red heart after the exclamation mark.`

## Failure modes
| Symptom | Fix |
|---|---|
| Garbled long copy | cut to a few words; split into elements |
| 9:16 needed on 4.5 | 4:7 then crop, or use v3 (9:16) |

## Self-check
- [ ] Quoted text in the first sentence
- [ ] No negations; style_type set on v3

Sources: Ideogram official docs (text early + quotes, avoid negatives; via search summary).
