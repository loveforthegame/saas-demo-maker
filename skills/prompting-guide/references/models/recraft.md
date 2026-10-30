# Recraft V3

**Model facts (at the time of writing; confirm in your provider):** aspect 1:1, 4:3, 3:4, 3:2,
2:3, 16:9, 9:16, 4:5, 5:4. A **style** setting picks the medium: any, realistic image (with
substyles such as natural light, studio portrait, black and white, HDR) or digital illustration
(with substyles such as pixel art, hand drawn, 2D art poster). The API enum values are named like
`realistic_image` and `digital_illustration`; names may differ by provider. No references. Cheap.
Some providers return raster only even though Recraft can make vectors.

Check the provider's model options for the exact parameter names (style, substyle, aspect, output
format).

## When to pick it

- **Use for:** flat illustration, icons, brand marks, posters with controlled palettes, text
  placed at a position.
- **Not for:** edits, character consistency (no refs).

## Compile

- **Medium:** set it in the style setting, not in words.
- **Slot order:** subject -> composition -> palette (hex) -> line/shape rules -> text with
  placement.
- **Length:** 20 to 70 words.
- **Palette:** 3 to 4 hex values; ask for a plain background.
- **Text:** `Text "[EXACT]" in [font style] at [position].`
- **References:** none.

```
[Subject], [composition], flat shapes, [line weight], limited palette #RRGGBB, #RRGGBB, #RRGGBB,
plain [colour] background. Text "[EXACT]" in [font style] at [position].
```

### Example

Bad: `cool vector logo, colorful, modern, no gradients`
Good (style = digital illustration): `A boxing glove icon seen from the side, centred, flat shapes,
2px uniform outline, palette #1F4FA0, #F2C230, #FFFFFF, plain white background.`

## Self-check

- [ ] Style set; palette as hex; plain background

## Failure modes

| Problem | Fix |
|---|---|
| Wrong medium | set the style; do not describe it |
| Muddy palette | 3 to 4 hex values, plain background |

## Field notes

Name the flat style, line weight and palette as hex. If the provider lists a vector or style
option, set it rather than describing it. General image rules live in image-others.md.

Sources: Recraft V3 API reference (text positioning); Recraft prompt tips (flat shapes, limited
palette); internal production field notes.
