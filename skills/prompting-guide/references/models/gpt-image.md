# GPT Image (GPT Image 2, GPT Image 2.5 Sunburst, GPT Image 2.5 Flare)

**Model facts (at the time of writing; confirm in your provider):** sizes from 1024x768 up to
2160x3840 (11 sizes, e.g. 1080x1920 for 9:16); quality low / medium / high (2.5 adds xhigh and
max). Up to 5 reference images. Up to 4 outputs per call on some providers. Mid cost at default
quality.

Check the provider's model options for the exact parameter names (size, quality, reference slots).

## When to pick it

- **Use for:** anything with words that must be right (posters, thumbnails, ad cards, UI mocks,
  infographics, banners), identity-sensitive edits, layout-heavy design. Default text model;
  2.5 Flare is the premium text option.
- **Not for:** 14-ref composites (Nano Banana).

## Compile

- **Slot order:** use (stated first) -> background/scene -> subject -> key details -> text ->
  constraints. For complex requests use short labelled segments.
- **Length:** any; must-haves first.
- **Layout:** write it like a designer's brief: grid, hierarchy (headline, subhead, CTA), exact
  copy in quotes, brand colours as hex, safe margins.
- **Text:** in quotes or ALL CAPS; give font, size, colour, placement; spell tricky words letter by
  letter ("P-R-E-D-I-S"); demand verbatim, appears once.
- **Quality:** high (or xhigh on 2.5) for small or dense text, close portraits, identity edits.
- **Size:** sizes above 2560x1440 are less stable; generate at 1080x1920 for Reels.
- **References:** refer by index and description ("image 1: the product; image 2: the style").
  For compositing say where it goes and to match light, perspective, scale and shadow.
- **When a reference carries it:** drop the description of the referenced product or style; keep
  its role and placement.
- **Edits:** name the region and the change: "Change only X. Keep everything else the same." Repeat
  the full preserve list (layout, labels, colours, angle) on every iteration.

```
Use: [ad card for Instagram, 1080x1920].
Scene: [background].
Subject: [subject + pose].
Details: [materials, light, camera framing].
Text (verbatim, appears once): headline "[EXACT TEXT]" in [font style, weight, colour hex], [placement].
Constraints: [what must stay / not appear, said positively]. No extra text.
```

### Example

Bad:
> nice poster for a boxing event with text and a boxer, modern design

Good:
> Use: vertical event poster, 1080x1920. Scene: dark charcoal background with warm tungsten haze.
> Subject: a bearded heavyweight boxer in red gloves, waist up, lit from above. Text (verbatim,
> each appears once): headline "BEST LOSS EVER" in heavy condensed sans, white, top third,
> centred; subline "Sat 7 PM, Eastside Gym" in medium sans, #F2C230, under the headline. No other
> text.

## Self-check

- [ ] Use + size stated; text quoted with font, colour, placement
- [ ] Quality high or above when text is small or a face matters
- [ ] Preserve list on edits

## Failure modes

| Problem | Fix |
|---|---|
| Misspelled brand | spell it letter by letter; quality high |
| Drift over edit rounds | repeat the whole preserve list every round |
| Extra stray text | "No other text"; one text block per element |

## Field notes

General image rules (editing, text, consistency across a set) live in image-others.md.

Sources: OpenAI cookbook "GPT Image Generation Models Prompting Guide"; internal production field
notes.
