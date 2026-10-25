# Character and prop reference sheets

Source: "AI Character Sheet Guide" (promptwise-free /16).

Use before any multi-shot video with a recurring character or product. The sheet becomes the reference image passed on every shot.

## Three rules

1. **Three-panel layout**: 16:9 canvas, three equal panels in one row. Same identity, outfit and proportions in all three.
   - Close-up: head and shoulders, facial features easy to read.
   - Front full-body: head to toe including shoes, outfit and proportions.
   - Back full-body: same outfit and scale, hair, clothing and rear silhouette.
2. **Neutral lighting**: plain neutral grey background, soft even light, visible skin texture, no glare or blown highlights. (White works if exposure is controlled; grey doesn't fix bad light by itself.)
3. **One clear face reference**: after generation, hide the facial features in the front full-body panel so the close-up is the only detailed face. Reduces competing face references (results still depend on the video model).

## Character sheet prompt

Set 16:9 in the generator settings.

```
[Describe your character: age, face, hairstyle, build, outfit and shoes.]
Create a 16:9 character sheet with three equal-width panels in one horizontal row on a flat neutral grey studio background. Use soft, even lighting, balanced exposure and visible natural skin texture. No environment, props or text labels. No hard shadows on the backdrop.
Panel 1: front-facing close-up of the head and shoulders, with clearly defined facial features.
Panel 2: full body, front view, neutral standing pose, head and shoes fully visible.
Panel 3: full body, back view, same standing pose and scale, head and shoes fully visible.
Keep the same identity, hairstyle, body proportions, outfit, materials and colors across all three panels.
```

## Face edit (image editor or editing model)

```
Edit only the front full-body panel. Hide its facial features with a flat grey color matching the backdrop. Preserve the hair, head outline, neck, body and clothes. Leave the close-up portrait and back view unchanged.
```

## Prop sheet prompt

```
[Describe your prop: shape, material, color and distinctive details.]
Create a 16:9 two-panel prop sheet on a flat neutral grey studio background. Use soft, even lighting. No environment or text labels. No hard shadows on the backdrop.
Panel 1: front-facing close-up of the prop, showing its distinctive details.
Panel 2: full shot of the entire prop, fully inside the frame.
Keep the same shape, materials, colors and proportions in both panels.
```

Generate at a high-quality setting. Check sharpness, matching outfit/materials and complete framing before using it for video.

Pair with the CAST line and REFERENCES line rules in [realism.md](realism.md).
