# Seedream (`seedream_5_pro`, `seedream_4_5`, `seedream_5_lite`)

**Predis options:**
- `seedream_5_pro`: t2i only, `resolution` 1K|2K, aspect 16:9|9:16|1:1|4:3|3:4. 5 cr.
- `seedream_4_5`, `seedream_5_lite`: `aspect` 1:1|4:3|3:4|16:9|9:16|3:2|2:3|21:9; refs up to 10
  images. 3 cr.

**Use for:** character turnaround sheets from one reference, illustration and design work,
cheap consistent sets, small legible text (4.5+).
**Not for:** edits on 5 Pro (no refs).

## Compile

Order: **subject -> action/pose -> setting -> style -> composition -> text**. 40 to 120 words, full
sentences. Name things; no pronouns in edits ("the woman's jacket", not "her jacket" or "it").

```
[Subject trait line or "the woman in image 1"] [pose]. [Setting]. [Style medium]. [Composition].
Text: "[EXACT]" in [style], [placement].
```

- Refs: start with 1-3; more refs only if consistency improves.
- Turnaround: "character turnaround sheet of the man in image 1: front, three-quarter, side,
  back, neutral pose, plain light grey background, identical outfit in every view, small labels
  under each view".

## Good vs bad
Bad: `make her different and put it somewhere else`
Good: `Change the woman's denim jacket to a red satin bomber jacket. Keep her face, pose, the
street and the light identical.`

## Failure modes
| Symptom | Fix |
|---|---|
| Edit hits the wrong object | replace pronouns with names |
| Inconsistent sheet views | "identical outfit in every view", plain background |

## Self-check
- [ ] No pronouns in edit instructions
- [ ] 5 Pro used only for t2i

Sources: BytePlus ModelArk Seedream guide (quoted text, via Hedra), EvoLink Seedream guide.
