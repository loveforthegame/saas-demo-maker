# Motion: frame rate and shutter

Source: "The AI Motion Cheat Sheet" (promptwise-free /23).

When AI action looks like a video game, the frames are fine but the motion is too clean and gliding, blurred in the wrong places, or slowed when nobody asked. Name the frame rate and shutter AND what the viewer sees. The model has no shutter; the numbers describe a look it learned. Output frame rate is whatever the tool delivers (e.g. 24 fps for Seedance 2.5).

## The three core looks

| Look | Write | Viewer sees |
|---|---|---|
| Film blur | 24 fps, normal 180-degree shutter (1/48 s) | Soft natural streaks on fast motion. Default for most scenes |
| Frozen | 24 fps, very fast 1/1000 s shutter, played at real speed | Every drop crisp and separate, slightly choppy. Rain, splashes, fights, sparks |
| Slow motion | Shot at 120 fps, played back at 24 (1/240 s shutter) | 5x slower, smooth, fine readable detail. For the one moment to stretch |

## Shutter at 24 fps

| Shutter | Speed | Motion |
|---|---|---|
| 360° | 1/24 s | Heavy smeary trails, dreamy or drunk |
| 180° | 1/48 s | Natural film blur |
| 90° | 1/96 s | Crisper, slightly nervous |
| 45° | 1/192 s | Sharp, staccato (war-film battle look) |
| ~9° | 1/1000 s | Frozen, crisp, slightly choppy |

Normal shutter = 1 / (2 x frame rate). Angle to speed: angle / 360 / fps.

## Motion blocks

**Film blur**
```
Shot at 24 frames per second with a normal 180-degree shutter (1/48 second), so everything moving fast relative to the camera carries soft, natural motion blur, like real 35 mm film. [The subject] stays [steady and readable], while [the fast things, e.g. hands, hair, wheels, the background] smear with soft, natural motion blur.
```
Blur comes from movement relative to the camera. Tracking at the subject's speed keeps the subject sharp and smears the background; a static camera does the opposite. Say which. Pan slowly at 24 fps or follow a subject; fast pans stutter.

**Frozen**
```
Shot at 24 frames per second with a very fast 1/1000-second shutter and played at real speed, not slow motion. There is no motion blur anywhere: every [raindrop, splash, spark or grain of dust] is a crisp, separate bead instead of a streak, and the motion is slightly choppy and staccato.
```
Frozen is not slow motion: repeat "played at real speed, not slow motion" in the shot line too. Backlight the rain so drops glint.

**Slow motion**
```
Shot at [120] frames per second (a [1/240]-second shutter) and played back at 24, so all motion, including the camera's, runs [five] times slower than life: smooth and crisp, with [the detail to read, e.g. every wingbeat] readable and only the faintest softness on the fastest parts.
```

| Shoot at | Slowdown | Good for |
|---|---|---|
| 48 fps, 1/96 | 2x | Gentle dreamy walking, dancing |
| 60 fps, 1/120 | 2.5x | Hair, fabric, sport |
| 120 fps, 1/240 | 5x | Birds, splashes, hair flicks, reveals |
| 240 fps, 1/480 | 10x | Water, breaking glass, sparks |

- Count real seconds: 5 s clip at 5x = 1 s of real action. Pick a ~1 s action.
- Slow the camera too: "everything, the camera included, moves five times slower than life".
- Generate slow motion; don't stretch normal footage in the edit (stutters or warps).
- Sound: describe deep, slowed-down sounds.

## Four more looks

**Dreamy smear**
```
Shot at 24 frames per second with a wide-open 360-degree shutter (1/24 second), so every movement leaves long, soft, smeared trails: [the moving things] streak and blend into each other, and the whole shot feels dreamy and a little unreal.
```
Keep it short; tiring to watch.

**Phone video (UGC)**
```
Filmed on a phone held in one hand at 30 frames per second in bright daylight, so the phone picks a very fast shutter and the motion is crisp with almost no blur. Slight natural handheld shake, small focus and exposure shifts as [the person] moves, and no cinematic camera moves.
```

**Speed ramp**
```
The shot starts at real speed with natural motion blur. At [the peak of the action] it ramps smoothly down to slow motion, as if shot at 120 frames per second and played back at 24, holds the moment for [two] seconds with every detail crisp, then ramps smoothly back up to real speed as [the person lands].
```
If the model plays one speed, make two clips and cut on the peak.

**Time-lapse**
```
Time-lapse from a camera locked on a tripod, about [one hour] squeezed into [five] seconds: [clouds race across the sky, shadows slide across the ground], and the crowds and traffic turn into soft, flowing streams, while [the buildings and the street] stay perfectly still. Smooth and steady, with no flicker.
```

## WEAK → BETTER

WEAK: A woman runs through a rainy night market, cinematic, epic action, smooth motion, 4k, ultra detailed.

BETTER: A woman runs through a rainy night market toward the camera, shot at 24 frames per second with a normal 180-degree shutter, so her arms, her hair, the passing crowd and the falling rain carry soft, natural motion blur, like real 35 mm film, while her face stays readable.

## Placement in the prompt

MOTION block goes near the top (after SET and LIGHT), and the key result is repeated in the SHOT line, because models lose the motion by the time they reach the action. LOOK ends with "No slow motion unless the shot asks for it."

## Fixes

| Problem | Change |
|---|---|
| Looks like a video game | Add film blur block, remove "smooth", "clean", "ultra detailed", name what blurs |
| Asked frozen, got slow-mo | "played at real speed, not slow motion" in MOTION and shot line |
| Slow-mo plays at normal speed | Give slowdown as a number (5x), shorter action |
| Subject blurs, should be sharp | Track at subject's speed, "subject stays steady and readable" |
| Everything smears, even faces | Back to 180°, name only fast things as blurred |
| Camera at normal speed in slow-mo | "everything, the camera included, moves five times slower" |
| Fast pan stutters | Slow the pan or follow a subject |
| Slowed footage warps | Generate the slow motion, don't stretch |

Check: step frame by frame through the fastest moment.
