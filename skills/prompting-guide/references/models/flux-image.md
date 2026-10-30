# FLUX images (FLUX.2 Pro / Flex / Max, FLUX 3 Image, FLUX 1.1 Pro Ultra, FLUX 1.1 Pro, FLUX.1 dev, FLUX.1 schnell)

**Model facts (at the time of writing; confirm in your provider):**
- FLUX.2 Pro / Flex / Max: 0.5 to 4 MP; 1:1, 16:9, 3:2, 2:3, 4:5, 5:4, 9:16, 3:4, 4:3; up to 10
  refs. Pro is cheap (the workhorse); Flex and Max are mid; Max is the top tier.
- FLUX 3 Image: 768 px to 4K; auto + 15 ratios; a grounding option (on by default on some
  providers); up to 10 refs (min 256 px). Mid.
- FLUX 1.1 Pro Ultra: 9 ratios; a reference strength setting (0 to 1, default 0.75); 1 ref. High-
  resolution photographic output. Mid.
- FLUX.1 dev: aspect, reference strength, 1 or 0.25 MP; 1 ref (ignores aspect with a ref). Cheap.
- FLUX 1.1 Pro: 1 ref. Cheap. FLUX.1 schnell: text to image only; near free; drafts.

Check the provider's model options for the exact parameter names (megapixels / resolution,
aspect, reference strength, guidance, reference slots).

## When to pick it

- **Use for:** strict prompt adherence, product colour accuracy (hex), cheap workhorse stills
  (FLUX.2 Pro), photographic high-res (1.1 Pro Ultra), near-free composition drafts (schnell),
  a different look from the Nano Banana family, cheap vector-ish marks when Recraft is not
  available.

## Compile

- **Slot order matters most here:** subject -> action -> style -> context -> secondary details.
  Earlier words weigh more.
- **Length:** 30 to 80 words; 80+ only for complex scenes.
- **No negative prompts.** Write what is there: "sharp focus throughout", "empty sky".
- **Hex colours:** write "color #RRGGBB" tied to one specific object. Never "use #X somewhere".
- **Photoreal:** name camera, lens, film stock; era cues ("2000s digicam") work.
- **Text:** quoted, with placement, size and colour.
- **JSON prompts** are equally understood: keys `scene`, `subjects` [{description, position,
  action}], `style`, `color_palette`, `lighting`, `mood`, `background`, `composition`, `camera`
  {angle, lens, depth_of_field}.
- **References:** "subject from image 1, style from image 2, background from image 3".
  Reference strength (1.x, if exposed): 0.3 to 0.5 loose inspiration, 0.75 default, 0.9
  near-copy.
- **When a reference carries it:** drop the description of what the ref supplies; keep its role.
- **Sequential panels:** full character description verbatim in every panel.

```
[Main subject] [key action], [critical style: "shot on 35mm film, 85mm f/1.4"], [essential
context]. [Secondary details]. [Colours: "the gloves in color #1F4FA0"].
```

### Example

Bad: `a bottle, no blur, no text, no people, professional photo, 8k`
Good: `A matte black insulated bottle stands on wet slate, condensation beading on its surface,
shot on Fujifilm X-T5 with a 35mm f/1.4, soft box from upper left, background a deep teal
gradient in color #0F4C5C, sharp focus throughout.`

## Self-check

- [ ] Subject first; 30 to 80 words; zero "no X"
- [ ] Every hex attached to an object

## Failure modes

| Problem | Fix |
|---|---|
| Excluded object appears | delete the negative, describe the replacement |
| Wrong brand colour | hex tied to the object with the "color" keyword |
| Late detail ignored | move it earlier |
| Output looks burnt (harsh contrast) | lower guidance, if the provider exposes it |

## Field notes

- Draft compositions on schnell before paying for a final; don't expect good text or fine detail
  from it (see image-others.md for draft rules).
- General image rules live in image-others.md.

Sources: BFL "Prompting guide FLUX.2" (docs.bfl.ai); internal production field notes.
