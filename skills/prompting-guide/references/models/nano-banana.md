# Nano Banana (Nano Banana Pro, Nano Banana 2, Nano Banana 2.1)

**Model facts (at the time of writing; confirm in your provider):** 1K, 2K or 4K; aspect 1:1, 4:5,
16:9, 9:16 (2.1 adds 5:4, 4:3, 3:4, 3:2, 2:3, 21:9, 9:21, 4:1, 1:4, 8:1, 1:8). Up to **14
reference images**. Up to 4 outputs per call on some providers. Cost: Pro is mid; 2 is cheaper;
2.1 is the cheapest.

Check the provider's model options for the exact parameter names (resolution, aspect, number of
outputs, reference slots).

## When to pick it

- **Use for:** photoreal keyframes for video, character and set references, multi-ref composites
  (person 1 in outfit 2 in place 3), consistent edits, product stills with a product ref,
  structured layouts via JSON. Default for photoreal, product and edits; Nano Banana 2 / 2.1 for
  cheaper takes.
- **Not for:** long typeset copy (GPT Image or Ideogram).

## Compile

- **Form:** it reasons before rendering. Write natural-language sentences, never tag lists.
- **Slot order:** intent/use -> subject (trait line) -> action/pose -> setting ->
  composition/camera -> light -> style -> text -> constraints. Say up front what the image is for
  ("first frame of a vertical video shot").
- **Length:** 50 to 150 words.
- **References:** number by the reference list order, one role each, and say what not to take from
  each: "image 1 is the model's face, image 2 is the jacket, image 3 is the location; put the
  woman from image 1 in the jacket from image 2 in the place from image 3". Keep a product image
  clean (plain background, label facing camera).
- **Text:** quoted text renders well for short headlines; keep body copy out.
- **Keyframes for video:** freeze a stable, readable start state, not mid-air action. The video
  model animates from it.
- **Edits:** "Change only X. Keep pose, expression, framing, light and everything else identical."
  Name what fills a removed area.
- **When a reference carries it:** drop the description of anything the refs show (face, outfit,
  set); keep only role + what must not transfer.

```
[Use: "Vertical 9:16 film still, first frame of a video shot."] [Ref roles: "Use the boxer from
image 1 and the boy from image 2, faces and outfits identical; the gym from image 3."]
[Subject + pose/action frozen at a stable moment]. [Composition: shot size, angle, where each
subject sits, what fills the foreground/background]. [Light sources]. [Look line].
```

### Example

Bad:
> boxer, kid, gym, boxing, cinematic, 8k, ultra detailed, masterpiece

Good:
> Vertical 9:16 film still, the first frame of a video shot. Use the boxer from image 1 and the
> boy from image 2 with faces and outfits identical, inside the gym from image 3. Wide low-angle
> shot from a ring corner: the giant boxer stands in the centre of the ring facing the small boy,
> both with gloves up, the boy reaching only to the boxer's belt. Schoolkids in yellow t-shirts
> crowd the red ropes behind them. Warm tungsten overheads, dust in the beams. 35mm film, shallow
> depth of field, soft grain.

## Self-check

- [ ] Use/intent stated first; full sentences
- [ ] Refs numbered in reference list order with roles
- [ ] Keyframes are stable start states
- [ ] Aspect matches the video aspect

## Failure modes

| Problem | Fix |
|---|---|
| Identity drifts across stills | same refs every time, re-anchor on the ORIGINAL ref, trait line verbatim |
| Two copies of a person | headcount line; one ref per person |
| Mid-action frame animates badly | regenerate as a stable start state |
| Angle-change edit fails | new generation from refs instead of editing |

## Field notes

### Structured JSON prompts

For precise, repeatable layouts (product hero, social graphic, UI mock, infographic, chart),
write the brief as JSON and pass it as the prompt with one lead line: "Render this specification
as one high-fidelity image." Every element gets a stable key, so the next edit changes one field
and leaves the rest alone, and A/B tests differ by exactly one value.

```json
{
  "type": "product_hero",
  "subject": {"product": "matte black insulated bottle", "label": "keep exactly as image 1", "position": "center, slightly left"},
  "props": [{"item": "sliced lime", "count": 2, "where": "foreground right"}],
  "environment": {"surface": "wet slate", "background": "deep teal gradient", "mood": "fresh, early morning"},
  "camera": {"angle": "three-quarter front", "framing": "medium close", "lens": "85mm", "depth_of_field": "shallow"},
  "lighting": {"key": "soft box upper left", "rim": "cool, from behind right", "color_temp": "5600K"},
  "text": [{"content": "STAY COLD 24H", "font": "bold condensed sans", "where": "top center"}],
  "aspect": "4:5",
  "locked": ["label", "bottle shape"]
}
```

Type ideas: `product_hero`, `social_graphic` (platform, background, text layers, logo spot),
`ui_mock` (platform, colour tokens, screens, components), `diagram` (nodes, edges, direction),
`chart` (type, exact data values, axes). Use JSON only when there is a defined target; for open
exploration plain prose gives more surprise. Valid JSON only, no comments.

General image rules (editing, text, consistency across a set) live in image-others.md.

Sources: Google AI Studio Nano Banana Pro tips (natural language over tags, 14 refs; via secondary
reports); internal production field notes.
