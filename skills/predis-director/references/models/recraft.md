# Recraft V3 (`recraft_v3`)

**Predis options:** `aspect` 1:1|4:3|3:4|3:2|2:3|16:9|9:16|4:5|5:4; **`style`** any |
realistic_image (+ natural_light, studio_portrait, b_and_w, hdr) | digital_illustration (+
pixel_art, hand_drawn, 2d_art_poster). No refs. 3 cr. Raster output via Predis.

**Use for:** flat illustration, icons, brand marks, posters with controlled palettes and text placed
at a position.
**Not for:** edits, character consistency (no refs).

## Compile

Set the medium in `style`, not in words. Prompt: **subject -> composition -> palette (hex) ->
line/shape rules -> text with placement**. 20 to 70 words.

```
[Subject], [composition], flat shapes, [line weight], limited palette #RRGGBB, #RRGGBB, #RRGGBB,
plain [colour] background. Text "[EXACT]" in [font style] at [position].
```

## Good vs bad
Bad: `cool vector logo, colorful, modern, no gradients`
Good (style = digital_illustration): `A boxing glove icon seen from the side, centred, flat shapes,
2px uniform outline, palette #1F4FA0, #F2C230, #FFFFFF, plain white background.`

## Failure modes
| Symptom | Fix |
|---|---|
| Wrong medium | set `style`; do not describe it |
| Muddy palette | 3-4 hex values, plain background |

## Self-check
- [ ] `style` set; palette as hex; plain background

Sources: Recraft V3 API reference (text positioning), Recraft prompt tips (flat shapes, limited
palette).
