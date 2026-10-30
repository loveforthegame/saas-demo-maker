# Ideogram (Ideogram V3 Quality, Ideogram 4.5, Ideogram 4.5 Precise Edit)

**Model facts (at the time of writing; confirm in your provider):**
- Ideogram V3 Quality: 15 aspect ratios (incl. 9:16, 4:5, 3:1); a style type setting (None,
  Auto, General, Realistic, Design); up to 3 style reference images (text to image). Mid-to-
  premium.
- Ideogram 4.5: quality low / medium / high; aspect auto, 1:1, 10:7, 7:10, 7:4, 4:7, 12:5, 5:12
  (**no 9:16**: use 4:7 and crop); up to 5 refs. Mid.
- Ideogram 4.5 Precise Edit: image to image only; quality very low to high; 1 source image + up
  to 4 refs. Mid.

Check the provider's model options for the exact parameter names (style type, quality, aspect,
source and reference slots).

## When to pick it

- **Use for:** typography-led images (logos, wordmarks, posters, stickers), fixing text inside an
  existing image (Precise Edit).
- **Not for:** photoreal keyframes for video.

## Compile

- **Slot order:** format -> quoted text (near the start) -> lettering style -> placement ->
  imagery -> palette -> layout/background.
- **Length:** 20 to 80 words. Shorter text = fewer errors.
- **Text:** in quotes, with style ("hand-lettered brush script", "geometric sans, all caps, tight
  tracking"). Readable fonts; highly decorative lettering fails first.
- **No negative phrasing** ("no people", "without trees"): describe what fills the space.
- **Style (V3):** set the style type to Design for graphic layouts, Realistic for photo-like,
  rather than describing it in words.
- **Precise Edit:** source first in the reference list; `Change "OLD" to "NEW", keep font, colour
  and position.` Keep new text close in length to the old.
- **When a reference carries it:** a style ref sets the look; drop style words and keep the text
  and layout instructions.

```
[Format: poster | logo | sticker] with the text "[EXACT]" in [lettering style], [placement].
[Imagery]. [Palette]. [Layout/background].
```

### Example

Bad: `a poster without people, no clutter, write something about boxing`
Good: `Poster with the text "GO LEO!" in thick hand-painted brush letters, slightly uneven, centred
on torn brown cardboard, black marker outline, small red heart after the exclamation mark.`

## Self-check

- [ ] Quoted text in the first sentence
- [ ] No negations; style type set on V3

## Failure modes

| Problem | Fix |
|---|---|
| Garbled long copy | cut to a few words; split into elements |
| 9:16 needed on 4.5 | 4:7 then crop, or use V3 (9:16) |

## Field notes

General image rules (text editing, consistency) live in image-others.md.

Sources: Ideogram official docs (text early + quotes, avoid negatives; via search summary);
internal production field notes.
