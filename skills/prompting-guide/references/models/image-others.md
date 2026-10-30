# Other image models + rules for every image model

Covers Qwen Image 3, MAI Image 2.5, Grok Imagine Image 2, Krea 2 Turbo, P-Image, and the general
image rules every other image file points to.

**Model facts (at the time of writing; confirm in your provider):**
- Qwen Image 3: text to image; 1K or 2K; 16:9, 9:16, 1:1, 4:3, 3:4. Cheap. Slow (about 275 s in
  one test).
- MAI Image 2.5: text to image; 1:1, 4:3, 3:4, 16:9, 9:16, 3:2, 2:3. Mid-to-cheap.
- Grok Imagine Image 2: text to image + image to image; 1K or 2K; quality low or medium; 13
  aspects incl. 9:19.5; up to 3 refs. Mid.
- Krea 2 Turbo: text to image; 1K or 2K; 5 aspects. Near free.
- P-Image: text to image; 7 aspects. Near free.

Check the provider's model options for the exact parameter names.

## When to pick it

- **Use for:** an alternative look when the main models feel samey (MAI, Qwen), stylized bold
  stills (Grok), near-free drafts, moodboards and thumbnails to pick from (Krea, P-Image, also
  FLUX.1 schnell).
- **Not for:** text, fine detail or refs on draft models.

## Compile

No model-specific official guides were found at the time of writing. Use the universal image
grammar.

- **Slot order:** subject -> action -> setting -> composition -> light -> style.
- **Length:** 30 to 80 words, full sentences, positive phrasing only. Drafts: 15 to 40 words,
  composition and light only; no text, no refs.
- **References:** Grok Image only (up to 3).
- **When a reference carries it:** see the editing rules below.

```
[Subject] [action] in [setting]. [Shot size, angle]. [Light source]. [Style medium].
```

### Example

Bad: `boxer kid gym, 8k, trending`
Good (draft): `Wide low angle: a giant boxer faces a tiny boy in a boxing ring, kids at the ropes, warm
overhead light, film still.`

## Self-check

- [ ] Drafts used only to pick composition; final on a router default
- [ ] No text on draft models

## Failure modes

| Problem | Fix |
|---|---|
| Text garbled on drafts | drafts never carry text |
| Grok edit looks soft | quality medium; 3 refs or fewer |

## Field notes: rules for every image model

### Writing

- Full sentences, not tag lists. "A woman in a Tokyo alley at dusk, neon reflecting off wet
  pavement" beats "woman, Tokyo, alley, dusk, neon".
- Specific and spatial: exact colours, materials, light setup, lens, where things sit relative to
  each other.
- Photo vocabulary works: film stocks (Kodak Portra 800, Ilford HP5), lenses (85mm f/1.4, 24mm
  wide), depth of field, Rembrandt / rim / soft diffused / volumetric light, rule of thirds,
  symmetry, tilt-shift.
- Long, structured prompts are fine on current models; the more requirements, the more likely one
  is missed, so put the must-haves first.
- Start simple, then iterate with edits rather than rewriting from scratch.

### Editing (image to image)

- Say what stays: "keep the pose, expression, framing and camera angle identical; only replace
  the background with a beach at golden hour".
- Pick the verb: "transform" invites a full rework. Use "change her jacket to blue denim".
- Removal: say what fills the gap ("remove the lamp; bare white wall continues behind it").
- Background swap: describe the new light and time of day so the subject matches.
- Angle changes are the hardest edit; expect to try another model.
- Break big changes into steps (outfit first, then scene).

### Text rendering

- Exact text in double quotes, with font style, weight, placement: `poster title "BLUE NOTE
  SESSIONS" in bold condensed sans-serif, top third, centered`.
- Readable fonts; highly decorative lettering fails first.
- Editing text: `Change "SALE" to "NEW", keep font, color and position`. Keep the new text close
  in length to the old.
- Best text models: GPT Image 2 (default), GPT Image 2.5 Flare (premium), Ideogram V3 Quality
  (typography and logos).

### Consistency across a set

- One reference image of the character or product on every image, plus the same trait line word
  for word.
- Change setting, action, light; keep the character line.
- Storyboards: "2x2 grid, panel 1 ... panel 4 ...", repeating the character line in each panel,
  or one image per panel with the same references (safer).
- Product sets: same camera and light block pasted into every prompt; vary only props and
  background.

Sources: model option listings at the time of writing; internal production field notes. Log
learnings here after real runs.
