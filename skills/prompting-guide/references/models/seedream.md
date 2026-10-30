# Seedream (Seedream 5 Pro, Seedream 4.5, Seedream 5 Lite)

**Model facts (at the time of writing; confirm in your provider):**
- Seedream 5 Pro: text to image only (no references); 1K or 2K; 16:9, 9:16, 1:1, 4:3, 3:4. Mid
  cost.
- Seedream 4.5 and 5 Lite: 1:1, 4:3, 3:4, 16:9, 9:16, 3:2, 2:3, 21:9; up to 10 reference images.
  Cheap.

Check the provider's model options for the exact parameter names (resolution, aspect, reference
slots).

## When to pick it

- **Use for:** character turnaround sheets from one reference, illustration and design work,
  faces and character sheets, cheap consistent sets, small legible text (4.5 and later), stylized
  bold stills.
- **Not for:** edits on 5 Pro (no refs).

## Compile

- **Slot order:** subject -> action/pose -> setting -> style -> composition -> text.
- **Length:** 40 to 120 words, full sentences.
- **Names, not pronouns:** in edits write "the woman's jacket", not "her jacket" or "it".
- **Text:** `Text: "[EXACT]" in [style], [placement].`
- **References:** start with 1 to 3; add more only if consistency improves.
- **When a reference carries it:** refer to "the woman in image 1" instead of a trait line.

```
[Subject trait line or "the woman in image 1"] [pose]. [Setting]. [Style medium]. [Composition].
Text: "[EXACT]" in [style], [placement].
```

Turnaround template:
> character turnaround sheet of the man in image 1: front, three-quarter, side, back, neutral
> pose, plain light grey background, identical outfit in every view, small labels under each view

### Example

Bad: `make her different and put it somewhere else`
Good: `Change the woman's denim jacket to a red satin bomber jacket. Keep her face, pose, the
street and the light identical.`

## Self-check

- [ ] No pronouns in edit instructions
- [ ] 5 Pro used only for text to image

## Failure modes

| Problem | Fix |
|---|---|
| Edit hits the wrong object | replace pronouns with names |
| Inconsistent sheet views | "identical outfit in every view", plain background |

## Field notes

Turnaround sheets work on edit-capable versions only (4.5, 5 Lite): several angle views of one
character from a reference photo. General image rules live in image-others.md.

Sources: BytePlus ModelArk Seedream guide (quoted text, via Hedra); EvoLink Seedream guide;
internal production field notes.
