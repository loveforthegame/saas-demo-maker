# FLUX images (`flux_2_pro`, `flux_2_flex`, `flux_2_max`, `flux_3_image`, `flux_1_1_pro_ultra`, `flux_1_1_pro`, `flux_1_dev`, `flux_1_schnell`)

**Predis options:**
- `flux_2_pro|flex|max`: `resolution` 0.5|1|2|4 MP, aspect 1:1|16:9|3:2|2:3|4:5|5:4|9:16|3:4|4:3;
  refs up to 10. 2 / 5 / 6 cr.
- `flux_3_image`: `resolution` 768px-4K, aspect auto + 15 ratios, `grounding` bool (default true);
  refs up to 10 (min 256 px). 4 cr.
- `flux_1_1_pro_ultra`: aspect 9 ratios, **`ref_strength`** 0-1 (default 0.75), 1 ref. 5 cr.
- `flux_1_dev`: aspect, `ref_strength`, `megapixels` 1|0.25, 1 ref (ignores aspect with a ref). 2 cr.
- `flux_1_1_pro` (3 cr, 1 ref), `flux_1_schnell` (0.24 cr, t2i, drafts).

**Use for:** strict prompt adherence, product colour accuracy (hex), cheap workhorse stills
(`flux_2_pro`), photographic high-res (`ultra`), near-free composition drafts (`schnell`).

## Compile

Order matters most here: **subject -> action -> style -> context -> secondary details** (earlier
words weigh more). Length 30 to 80 words; 80+ only for complex scenes.

```
[Main subject] [key action], [critical style: "shot on 35mm film, 85mm f/1.4"], [essential
context]. [Secondary details]. [Colours: "the gloves in color #1F4FA0"].
```

- **No negative prompts.** Write what is there: "sharp focus throughout", "empty sky".
- Hex colours: write "color #RRGGBB" tied to one specific object. Never "use #X somewhere".
- Photoreal: name camera, lens, film stock; era cues ("2000s digicam") work.
- Text: quoted, with placement, size and colour.
- JSON prompts are equally understood: keys `scene`, `subjects` [{description, position, action}],
  `style`, `color_palette`, `lighting`, `mood`, `background`, `composition`, `camera` {angle,
  lens, depth_of_field}.
- Multi-ref: "subject from image 1, style from image 2, background from image 3".
- `ref_strength` (1.x): 0.3-0.5 loose inspiration, 0.75 default, 0.9 near-copy.
- Sequential panels: full character description verbatim in every panel.

## Good vs bad
Bad: `a bottle, no blur, no text, no people, professional photo, 8k`
Good: `A matte black insulated bottle stands on wet slate, condensation beading on its surface,
shot on Fujifilm X-T5 with a 35mm f/1.4, soft box from upper left, background a deep teal
gradient in color #0F4C5C, sharp focus throughout.`

## Failure modes
| Symptom | Fix |
|---|---|
| Excluded object appears | delete the negative, describe the replacement |
| Wrong brand colour | hex tied to the object with "color" keyword |
| Late detail ignored | move it earlier |

## Self-check
- [ ] Subject first; 30-80 words; zero "no X"
- [ ] Every hex attached to an object

Sources: BFL "Prompting guide FLUX.2" (docs.bfl.ai).
