# GPT Image (`gpt_image_2`, `gpt_image_2_5_sunburst`, `gpt_image_2_5_flare`)

**Predis options:** `output_size` 1024x768 ... 2160x3840 (11 sizes, e.g. 1080x1920 for 9:16);
`quality` low|medium|high (2: default medium) or low|medium|high|xhigh|max (2.5: default high).
Ref mode `references`: up to 5 images. Up to 4 outputs. 4 cr per image at default.

**Use for:** anything with words that must be right (posters, thumbnails, ad cards, UI mocks,
infographics), identity-sensitive edits, layout-heavy design.
**Not for:** 14-ref composites (Nano Banana).

## Compile

Order: **background/scene -> subject -> key details -> constraints**, with the intended use
stated up front. For complex requests use short labelled segments. Any length; must-haves first.

```
Use: [ad card for Instagram, 1080x1920].
Scene: [background].
Subject: [subject + pose].
Details: [materials, light, camera framing].
Text (verbatim, appears once): headline "[EXACT TEXT]" in [font style, weight, colour hex], [placement].
Constraints: [what must stay / not appear, said positively]. No extra text.
```

- Text: in quotes or ALL CAPS; give font, size, colour, placement; spell tricky words letter by
  letter ("P-R-E-D-I-S"); demand verbatim, appears once.
- Quality: high (or xhigh on 2.5) for small/dense text, close portraits, identity edits.
- Edits: "Change only X. Keep everything else the same." and repeat the full preserve list
  (layout, labels, colours, angle) on every iteration.
- Multi-ref: refer by index and description ("image 1: the product; image 2: the style"); for
  compositing say where it goes and to match light, perspective, scale and shadow.
- Sizes above 2560x1440 are less stable; generate at 1080x1920 for Reels.

## Good vs bad

Bad:
> nice poster for a boxing event with text and a boxer, modern design

Good:
> Use: vertical event poster, 1080x1920. Scene: dark charcoal background with warm tungsten haze.
> Subject: a bearded heavyweight boxer in red gloves, waist up, lit from above. Text (verbatim,
> each appears once): headline "BEST LOSS EVER" in heavy condensed sans, white, top third,
> centred; subline "Sat 7 PM, Eastside Gym" in medium sans, #F2C230, under the headline. No other
> text.

## Failure modes
| Symptom | Fix |
|---|---|
| Misspelled brand | spell it letter by letter; quality high |
| Drift over edit rounds | repeat the whole preserve list every round |
| Extra stray text | "No other text"; one text block per element |

## Self-check
- [ ] Use + size stated; text quoted with font/colour/placement
- [ ] Quality >= high when text is small or a face matters
- [ ] Preserve list on edits

Sources: OpenAI cookbook "GPT Image Generation Models Prompting Guide".
