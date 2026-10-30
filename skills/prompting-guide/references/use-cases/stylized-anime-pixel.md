# Anime, illustration, pixel art, sprites, tiles, icons

Markers: **[tested]** = generated and reviewed in a source test. **[untested]** = not run in a source test. Unmarked = the source gave no status (the presets and sprite templates here are unmarked).

## Triggers

"turn my video into anime", "make me a cartoon", "claymation version", "3D animated feature look", "watercolor", "comic book style", "pixel art", "16-bit", "retro game", "sprite sheet", "walk cycle", "game asset", "tileable texture", "parallax background", "game icon", "illustration", "put my character in this dance".

For season or VFX changes on real footage ("make it winter", "set it on fire"), see [edit-restyle.md](edit-restyle.md).

## Load these

| Need | File |
|---|---|
| Same character across frames and sheets | [character-consistency.md](character-consistency.md), [../styles/reference-sheets.md](../styles/reference-sheets.md) |
| Text on a title logo or icon | [text-logo-ui.md](text-logo-ui.md) |
| One-change edits and long-clip chunks | [edit-restyle.md](edit-restyle.md) |

The photoreal style files (film stocks, realism) do not apply to stylized looks. Light direction still helps ("soft studio lighting", "neon rim light").

Router shot types ([../model-router.md](../model-router.md)): `stylized-anime`, `restyle`, `vector-flat`, `character-sheet`, `motion-transfer`, `draft-still`.

Model notes (from the source skills; confirm on your provider):

| Job | Pick | Alternatives |
|---|---|---|
| Restyle real footage, premium | Runway Aleph 2 | Kling 3 Omni when faces smear or motion is fast; Seedance 2.0 only if it accepts a reference video |
| Restyle drafts, clay / watercolor / pixel, long clips | Wan 2.7 video edit | |
| Dance swap (character into a dance clip) | DreamActor M2 | |
| Sprite clip route (image to video) | Kling 2.5 Turbo (quality) | Wan 2.2 i2v fast (cheap draft) |
| Ground / wall tiles | FLUX 2 Pro or Recraft V3 | |
| Icons and UI art | Recraft V3 | GPT Image 2 for a title logo with text |

Model files: [video-edit-restyle](../models/video-edit-restyle.md), [kling](../models/kling.md), [wan](../models/wan.md), [seedance](../models/seedance.md), [flux-image](../models/flux-image.md), [recraft](../models/recraft.md), [gpt-image](../models/gpt-image.md).

## Recipe A: restyle a video

Video-to-video models follow short, concrete prompts best. Describe the target look, not the process. Say "the same" for anything that must survive.

Default keep line:
```
Keep the exact motion, timing, camera movement, framing and composition of the original video. Keep each person's pose, gestures and expressions.
```

| Preset | Prompt |
|---|---|
| Anime | `Restyle this video as a hand-drawn 2D anime scene: clean ink linework, cel shading with two-tone shadows, soft painted backgrounds, luminous sky, expressive anime eyes on {subject}. {keep} {extra}` |
| Watercolor anime | `Turn this video into a gentle hand-painted anime film look: watercolor backgrounds, soft pastel palette, warm afternoon light, delicate linework on {subject}, lush greenery. {keep} {extra}` |
| Claymation | `Make this video look like stop-motion claymation: {subject} made of smooth plasticine with visible thumbprints, slightly lumpy handmade sets, soft studio lighting, miniature depth of field. {keep} {extra}` |
| 3D animated feature | `Restyle this video as a high-end 3D animated feature film: {subject} as stylized 3D characters with big expressive eyes, soft subsurface skin, rounded forms, rich global illumination, cinematic color. {keep} {extra}` |
| Watercolor painting | `Turn this video into a moving watercolor painting: wet paper texture, soft bleeding edges, loose brush strokes, white paper showing through highlights, {subject} painted with visible pigment. {keep} {extra}` |
| Comic book | `Restyle this video as a comic book panel come to life: bold black ink outlines, halftone dot shading, flat saturated colors, dramatic shadows on {subject}. No speech bubbles, no text. {keep} {extra}` |
| Cyberpunk night | `Transform the setting into a rain-soaked cyberpunk city at night: neon signs in magenta and cyan, wet reflective streets, holographic haze, {subject} lit by neon rim light. No readable text. {keep} {extra}` |
| Pixel art / retro game | `Restyle this video as 16-bit pixel art from a retro video game: chunky visible pixels, limited palette, crisp dithering, {subject} as pixel sprites. {keep} {extra}` |

Custom style formula:
```
Restyle this video as <medium>: <3 to 5 visual traits: line, shading, palette, texture, light>, <how the subject looks>. {keep}
```
- Name a medium (anime, clay, oil paint, paper cutout, LEGO-like bricks), not an artist or studio. Do not name living artists or brands.
- One style per take. "Anime but also claymation" turns to mush.
- If the model has a strength or fidelity option, start mid-range. Low keeps more of the original; high restyles harder.
- Video-to-video output often drops the sound: put the original audio back in the edit.
- Long clips: see chunking in [edit-restyle.md](edit-restyle.md).

Dance swap (image 1 = the character, video 1 = the dance clip, order per the model file):
```
The character from the reference image performs the exact dance from the reference video: same moves, timing and rhythm. Keep the character's face, outfit, proportions and art style from the image. {extra}
```
Good input: full-body character image, front facing, arms visible, plain background, same framing as the dancer. A head-only photo fails for a full-body dance. Only the user's own photo or someone who agreed.

## Recipe B: sprites and game art

### Global rules (every sprite prompt)

- `Background is 100% solid flat magenta #FF00FF, no gradient, no floor, no shadow, no vignette.`
- `No text, no labels, no UI, no watermark, no speech bubbles, no frame borders.`
- Paste the art-bible STYLE BLOCK word for word.
- Name the camera: side view, top-down 3/4, or isometric.
- Name the facing: `facing right` for side-scrollers (the game flips it for left).
- Keep magenta and hot pink out of the character. If the design needs pink, switch the key color to flat green #00FF00 and say so in the prompt.
- If the model has a transparent-background option, you may use it, but still check the alpha.

### Identity lock across frames

1. Generate ONE master frame (idle, full body, centered, generous margin). Get a yes.
2. Pass it as reference image 1 on every later sprite call, and open the prompt with:
   `Image 1 is the exact character: keep the same silhouette, face, palette, costume, markings, proportions and art style. Change only the pose.`
3. Enemies and props in the same world: pass the hero as image 2 with `style reference only, do not copy the character`.

### Grid sheet (one action per sheet)

```
Image 1 is the exact character: keep the same silhouette, face, palette, costume and style. Change only the pose.
A <2x2 | 2x3 | 2x4> sprite sheet of <character> doing a <action> cycle, <camera>, facing right.
EXACTLY <N> equal cells in <R> rows and <C> columns, read left to right, top to bottom.
Frame 1: <pose>. Frame 2: <pose>. Frame 3: <pose>. Frame 4: <pose>.
Same character size and camera distance in every cell. Feet on the same line in every cell.
The whole character fits inside its cell with magenta margin on all four sides; nothing crosses a cell edge.
No borders or lines between cells. <STYLE BLOCK>
Background is 100% solid flat magenta #FF00FF. No text, no labels, no shadow.
```
Square sheets (2x2, 3x3, 4x4) come out cleanest on 1:1. For 2x4 ask for 2:1 (or the nearest ratio the model offers) so cells stay square. Never pack idle + run + attack in one generation.

| Action | Grid | Frames |
|---|---|---|
| idle | 2x2 | neutral, inhale (chest up), full breath, exhale settle. SUBTLE |
| walk | 2x2 | right leg forward, passing, left leg forward, passing |
| run | 2x3 | contact, down, passing, up, contact (other leg), passing. Arms opposite legs |
| jump | 2x2 | crouch, rising (legs tucked), apex, landing crouch |
| attack | 2x2 | wind-up, strike, follow-through, recover. Body only: no slash arc, no muzzle flash |
| hurt | 2x2 | impact, recoil, stagger, recover |
| death | 2x3 | hit, fall, ground, fade poses |
| projectile | 1x4 | same shape, small pulse only |
| impact FX | 2x2 | contact, expand, peak, fade |

Big effects (slash arcs, explosions) get their own FX sheet; baked into the body sheet they shrink the character.
Top-down 4-direction walk: a 4x4 with row 1 down, row 2 left, row 3 right, row 4 up; columns neutral, left foot, neutral, right foot. Rows 2 and 3 must be true mirrored profiles.

### Clip route (smoother loops, more than 6 frames)

Master frame on flat #FF00FF, side view, feet in the lower third, margin all round, as the start image. Then:
```
The same character runs in place facing right with a side-scroller stride, arms swinging, body centered, camera locked, no zoom, no pan, solid flat magenta background only, no ground, no particles.
```
Do: in place (treadmill), locked camera, one action. Don't: travel across the frame, camera moves, scenery, combos. Video models tint flat backgrounds; expect to tune the key.

### Tiles and parallax

Ground / wall tile:
```
Seamless tileable <grass-topped dirt | stone brick | lava rock> ground texture for a 2D side-scroller, orthographic front view, edges wrap perfectly left-right and top-bottom, even lighting, no vignette, no focal object, no shadows at the edges. <STYLE BLOCK>
```
Check by tiling it 2x2 and looking for seams.

Parallax layers (16:9; make the far layer first and pass it as a style reference for mid and near):
- far: `distant <mountains | city skyline> silhouette, low contrast, sky colours from the palette, wide, nothing in the lower third`
- mid: `mid-distance <trees | buildings>, horizontal band across the middle, left and right edges must match so it wraps`
- near: `foreground <bushes | pipes> along the bottom quarter only, on solid flat magenta #FF00FF above`, then key it.

### Icons

```
ONE isolated <coin | heart | key | sword> game icon, centered, fills 80% of a square canvas, thick dark outline, <STYLE BLOCK>, readable at 32 px, solid flat magenta #FF00FF background, no text, no shadow.
```
Title logo with the game name: a text-strong model, quote the exact title, on magenta, key it. Buttons and HUD bars: draw in code.

### Filled example (walk sheet)

```
Image 1 is the exact character: keep the same silhouette, face, palette, costume and style. Change only the pose.
A 2x2 sprite sheet of a small fox knight in a dented tin helmet and a short green cape doing a walk cycle, side view, facing right.
EXACTLY 4 equal cells in 2 rows and 2 columns, read left to right, top to bottom.
Frame 1: right leg forward. Frame 2: passing. Frame 3: left leg forward. Frame 4: passing.
Same character size and camera distance in every cell. Feet on the same line in every cell.
The whole character fits inside its cell with magenta margin on all four sides; nothing crosses a cell edge.
No borders or lines between cells. STYLE: 32x32-feel chunky pixel art, 16-colour palette of forest greens, rust orange and steel grey, 1-pixel dark outline, flat shading with one highlight tone.
Background is 100% solid flat magenta #FF00FF. No text, no labels, no shadow.
```

## Pitfalls → fixes

| Pitfall | Fix |
|---|---|
| Two styles blend into mush | One style per take |
| Restyle melts faces or smears fast motion | Try the alternative restyle model; shorter prompt; lower strength |
| Restyle adds new things | "no new people or objects, the background stays the same room, same expression" |
| Original motion lost | Paste the keep line; lower strength |
| Audio missing after restyle | Put the original audio back in the edit |
| Sprite changes size between cells | "Same character size and camera distance in every cell"; master frame as image 1 |
| Character crosses cell edges | "fits inside its cell with magenta margin on all four sides" |
| Pink fringe after keying | Keep magenta out of the character, or switch to green #00FF00 |
| Slash effects shrink the character | Separate FX sheet |
| Tile shows seams | "edges wrap perfectly left-right and top-bottom", "no shadows at the edges"; tile 2x2 to check |
| Clip sprite drifts across frame | "in place", "camera locked, no zoom, no pan" |
| Comic restyle adds speech bubbles | "No speech bubbles, no text" |
| Dance swap breaks the body | Full-body front-facing character image, arms visible, plain background |

<!-- Sources: anime-me SKILL.md and references/style-presets.md; game-studio references/sprite-prompts.md; cinematic-story-reel references/prompt-guide.md section 7 (restyle tail). -->
