# Product stills and product motion

Markers: **[tested]** = generated and reviewed in a source test reel. **[untested]** = not run in a source test. Unmarked = the source gave no status (the product-shoot mode templates are unmarked).

## Triggers

"product shot", "product photo", "packshot", "studio shot", "catalog image", "lifestyle image", "hands holding my product", "model wearing my product", "virtual try-on", "splash shot", "levitating product", "Pinterest pin", "hero banner", "carousel of my product", "ad creatives", "restyle this for Christmas", "product video", "the label is garbled", "the product changed shape".

## Load these

| Need | File |
|---|---|
| Light matched to the material, one main light | [../styles/light-direction.md](../styles/light-direction.md) |
| f/2.8 product pops with a readable room; macro | [../styles/aperture.md](../styles/aperture.md) |
| Foreground framing (a dish edge in the lower-left corner, clear air) | [../styles/depth.md](../styles/depth.md) |
| Frozen splash or spark (1/1000 s shutter), slow-mo pour | [../styles/motion-shutter.md](../styles/motion-shutter.md) |
| Air: keep it front-lit and clear for products; haze hurts product crispness | [../styles/atmosphere.md](../styles/atmosphere.md) |
| Film stocks: Kodak Gold is bad for true-color product shots; HP5 is no use when color is the point | [../styles/film-stocks.md](../styles/film-stocks.md) |
| Text, price, offer on the image | [text-logo-ui.md](text-logo-ui.md) |
| A creator holding it on video | [talking-head-ugc.md](talking-head-ugc.md) |

Router shot types ([../model-router.md](../model-router.md)): `product-still`, `product-motion`, `macro-texture`, `text-graphic` (copy on the image), `short-insert`, `draft-still`.

Model notes (product-shoot source): product fidelity with a reference photo → Nano Banana Pro ([../models/nano-banana.md](../models/nano-banana.md)); readable text on the image → GPT Image 2 ([../models/gpt-image.md](../models/gpt-image.md)); cheap drafts → Seedream 4.5 ([../models/seedream.md](../models/seedream.md)); cheaper default → a cheaper Nano Banana tier. Cheap single-beat inserts (macro press, prop drop, time-lapse) → Seedance 1.5 Pro [tested], fallback Kling 2.5 Turbo.

## Recipe: stills

### 1. Get a product photo

It is the single biggest quality lever. With no photo, describe the product in hard facts: category, material, color, size, packaging, label text.

### 2. Fidelity sentence, word for word, first in every prompt

```
Keep the product exactly as in image 1: shape, label, colors.
```
The product photo is reference 1. Extra references (model photo, scene, style image) come after it, in the same order the prompt mentions them.

### 3. Build order

1. Product invariant (fidelity sentence + material and scale)
2. Role (catalog image, Instagram ad, hero banner)
3. Setting and props
4. Light matched to the material
5. Camera: angle, lens feel, depth of field
6. Composition and copy-safe space
7. Brand tone
8. Guardrails: no extra text, no invented logos, no label changes

Never invent claims ("clinically proven", "best seller", prices) the user did not supply.

### 4. Light cues by material

| Material | Light |
|---|---|
| Glass / liquid | backlight, rim light, soft caustics, controlled reflections |
| Metal | strip-light highlights, hard rim, dark flags, crisp specular lines |
| Matte plastic / cardboard | large softbox, soft shadow, no over-gloss |
| Fabric | raking side light, visible weave, natural folds |
| Food / drink | soft directional window light, condensation or steam only if plausible |
| Jewelry | macro feel, dark cards, controlled sparkle |

### 5. Mode templates

**Studio packshot**
```
Keep the product exactly as in image 1: shape, label, colors. {product_name}, a {material} {category}, is the only object in frame, placed on {surface} against a seamless {background} background. {lighting}, soft realistic contact shadow. {angle} view, {lens_feel} lens feel, entire product in sharp focus. Product centered, filling about {fill}% of the frame, generous even margins. Premium commercial product photography, {brand_tone}. No props, no extra text, no added logos, label unchanged.
```
Defaults: 85mm lens feel, fill 70, "clean and minimal". Aspect 1:1 (marketplaces), 4:5 (feed).

**Lifestyle scene**
```
Keep the product exactly as in image 1: shape, label, colors. {product_name} sits on {surface} in {scene}, {time_of_day} light from {light_direction}. Surrounding props: {props_max_3}, kept secondary and slightly out of focus. The product is the sharpest element in frame, label facing camera and readable. {angle}, {lens_feel} lens feel, shallow depth of field. Product placed {position}, {negative_space_side} left open for copy. Authentic editorial lifestyle photography, {brand_tone}. Product colors unchanged by scene lighting. No extra text, no other brands, no duplicate products.
```
Vary scene, time of day and angle across variants; keep brand tone fixed.

**Close-up with a person (hands)**
```
Keep the product exactly as in image 1: shape, label, colors. Close-up of {person_descriptor} {action} {product_name}, {framing}. Natural relaxed grip, realistic hands with five fingers, {nail_style}. The product label faces camera, unobstructed by fingers. {background}, softly blurred. {lighting}, flattering soft skin light. {lens_feel} macro-portrait lens feel, focus on the product and fingertips. Authentic beauty / lifestyle commercial, {brand_tone}. No extra text, no jewelry covering the label.
```
Defaults: hands and product only, cropped at the wrist; 100mm.

**Moodboard pin (2:3)**
```
Keep the product exactly as in image 1: shape, label, colors. Vertical Pinterest-style {layout} in a {aesthetic} aesthetic: {product_name} with {complementary_objects}, arranged on {surface}. Palette of {palette}, {lighting}, soft film-like texture. Product is the focal point in the upper-middle of the frame. {text_clause} Tasteful, aspirational, save-worthy editorial image.
```

**Hero banner (16:9)**
```
Keep the product exactly as in image 1: shape, label, colors. Wide cinematic hero banner: {product_name} placed on the {product_side} third on {surface}, {scene_or_background}. {lighting}, subtle depth. The {copy_side} half is clean, low-detail negative space in {bg_color} for headline text. {lens_feel} lens feel, product sharp, background gently defocused. Premium {brand_tone} campaign look. {text_clause}
```

**Carousel** — write a style lock once and paste it in every slide:
```
STYLE: {palette}, {surface}, {lighting_direction} light, {lens_feel} lens, {brand_tone}, same color grade on every slide.
```
```
Keep the product exactly as in image 1: shape, label, colors. Slide {n} of {total} in a carousel. {slide_content}. {STYLE} {text_clause} Composition leaves a clean band at the {top_or_bottom} for swipe continuity.
```
Make slide 1, check it, then pass it as image 2 for the rest: "match the palette, light and grade of image 2".

**Ad creative pack**
```
Keep the product exactly as in image 1: shape, label, colors. Paid social ad, {placement} format. {product_name} {hero_treatment}, {scene_or_background}. {lighting}. Strong scroll-stopping first read: product large and sharp in the {product_zone}. {copy_zone} kept clean for text. {text_clause} {brand_tone}, high contrast, uncluttered.
```
Vary the hero treatment (held in hand / on pedestal / in use / exploded ingredients). For 9:16 keep the top 14% and bottom 20% free of product and text.

**Virtual try-on** (image 1 = product, image 2 = model photo, optional)
```
Keep the product exactly as in image 1: shape, label, colors, pattern, hardware and fit details. {model_clause} wearing the {product_name} from image 1, {styling_notes}. {pose}. Setting: {setting}. {lighting}. {framing}, {lens_feel} lens feel, fashion editorial photography, realistic fabric drape and fit, true-to-life proportions. The product is the hero of the outfit, fully visible. No extra logos, no text.
```

**Conceptual (levitating, splash, exploded ingredients)**
```
Keep the product exactly as in image 1: shape, label, colors. {product_name} {concept_action}, {concept_elements} frozen in mid-air around it. {background}, {palette}. {lighting}, crisp high-speed-photography detail, {render_feel}. Product perfectly upright, undistorted and sharp; effects stay around it, never on the label. Centered composition, {aspect_notes}. High-end conceptual advertising image. No text.
```

For seasonal restyles of an existing product image, see [edit-restyle.md](edit-restyle.md).

### 6. Check before showing

Shape and cap match image 1; label is the real label; colors not shifted by scene light; exactly one product, not cropped; no stray text or fake logos.

## Recipe: product motion

1. **Still first.** Make the product still with the fidelity sentence and check it. Use it as the first frame.
2. **Write the still as the first frame of the move**, not the best moment:
   - Push-in: product small, the detail you will land on visible and lit.
   - Object to lens: the object visible near the subject, on a path toward the camera.
   - Time-lapse: locked-off, empty sky band, no people moving.
   - Screens in a product shot: "an even cool white glow". Real UI goes in during the edit; video models garble UI text [tested].
3. **One action, beat by beat, one camera move with a start and an end** (i2v pattern in [cinematic-story.md](cinematic-story.md)) [tested 7/7].
4. **Object-to-object actions** (a pour into a glass, a cap twisting off, a drop hitting a surface): one action per short shot, the action written with seconds, the key result repeated ("every drop a crisp separate bead"). Use the frozen or slow-motion block from motion-shutter.md. Write slow motion as a generated ramp, never a stretch in the edit.
5. **An object that hits or crosses the lens** must be sharp with visible detail; prompt the focus pull explicitly. A blurry blob was rejected. As a hidden cut: `the {object} swoops at the lens and fills the frame at {3.4}s` [tested].
6. Keep "Keep the product exactly as in image 1" in the video prompt too, and end with `No text, no subtitles, no watermark.`

### Filled example (still, lifestyle)

```
Keep the product exactly as in image 1: shape, label, colors. A 50 ml amber glass serum bottle with a black dropper cap sits on a pale travertine bathroom shelf in a small sunlit bathroom, early morning light from the left window. Surrounding props: a folded white linen towel, a small sprig of eucalyptus, a ceramic dish, kept secondary and slightly out of focus. Backlight through the glass and a soft rim light, soft caustics on the stone, controlled reflections. The product is the sharpest element in frame, label facing camera and readable. Three-quarter view, 85mm lens feel, shallow depth of field. Product placed on the right third, left side left open for copy. Authentic editorial lifestyle photography, calm and minimal. Product colors unchanged by scene lighting. No extra text, no other brands, no duplicate products.
```

### Filled example (motion, i2v from that still)

```
@Image1 is the first frame; preserve the bottle, its label and cap exactly. 0-1s: hold, the light shifts slightly across the stone. 1-3s: a hand enters from the right, lifts the dropper and lets a single drop fall back into the bottle; the drop is sharp with a bright highlight. 3-4s: the hand leaves frame. One slow push-in from a medium shot to a close-up of the label, ends with the label filling the centre third. Keep the product exactly as in image 1: shape, label, colors. No text, no subtitles, no watermark.
```
(`@Image1` is one tag style; use the model's own syntax from [../models/](../models/).)

## Pitfalls → fixes

| Pitfall | Fix |
|---|---|
| Label garbled or re-spelled | Quote the label text ("label reads 'GLOW 30ml'"); if still wrong, move that take to a text-strong model (GPT Image) |
| Shape drifts (taller, rounder, wrong cap) | Pass the product photo again as image 1, add "same silhouette and proportions as image 1", simplify the scene |
| Product looks redesigned or "improved" | Fewer adjectives, remove object style words ("sleek", "futuristic"), use the lowest creativity / highest reference strength option the model lists |
| Colors shift under warm or colored light | "product colors unchanged by scene lighting", colored light on the background only |
| Two products appear | "exactly one [product]", remove plural props |
| Hands look wrong | Tighter crop, fewer fingers visible, "natural relaxed grip", "one hand only" |
| Fingers cover the label | "hold from the base / sides, label fully visible" |
| Background not flat in a packshot | "seamless infinity cove, no horizon line, no gradient" |
| Shadow too heavy | "faint soft contact shadow only" |
| Props steal focus | Max 3 props, "props out of focus" |
| Product too small | "product occupies the lower third, about 30% of frame height" |
| Splash covers the label | "liquid splashes behind and below the product only" |
| Product melts or warps in a concept shot | Drop "surreal" / "dreamlike"; describe the elements literally |
| Carousel slides drift in color | Re-pass slide 1 as a reference |
| Screen in a product video shows garbage UI | "an even cool white glow"; real UI in the edit [tested] |
| Object on the lens is a blurry blob | Ask for sharp focus and visible detail on it; prompt the focus pull |

<!-- Sources: product-shoot SKILL.md and references/modes.md (adapted from higgsfield-ai/skills higgsfield-product-photoshoot, MIT); cinematic-story-reel references/prompt-guide.md sections 1, 3, 4 and 10 (tested in an internal test reel); promo-film-rules section 9 (object on the lens); saas-demo-maker SKILL.md generation rules (slow motion as a generated ramp); prompt-styles light-direction, aperture, depth, motion-shutter, atmosphere, film-stocks (PromptWise free guides, fetched 2026-10-20). -->
