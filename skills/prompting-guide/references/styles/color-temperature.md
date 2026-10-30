# Color temperature (Kelvin)

Source: "The Color Temperature Cheat Sheet" (promptwise-free /22).

Problem it solves: "at night" without a named light makes the model default to bright neutral white, so night looks like day with a darker sky. Fix: name the source, its Kelvin number, what it does, and what light is NOT there. A number alone is weak; a number next to a familiar source pins the look.

## The four numbers

| Kelvin | Light | Looks like | Use for |
|---|---|---|---|
| 2700 K | Candlelight | Warm flickering orange-gold on faces, fast falloff into deep warm shadow | Candlelit dinners, haunted houses, romance, flame |
| 3200 K | Tungsten lamp | Steady cozy golden amber, more yellow and less orange than candle | Living rooms at night, old offices, bars, interiors after dark |
| 5600 K | Daylight | Clean neutral, whites stay white, true colors | Midday exteriors, sunny streets, natural look |
| 8000 K | Cold blue night | Blue-white highlights, navy shadows, cool skin (film moonlight) | Night exteriors, snow, winter, suspense, loneliness |

Lower number = warmer. Looks assume camera balanced for daylight.

In-between (approximate): ~1900 K bare candle flame up close; 2700 K warm household bulb; ~3000-3500 K golden hour; ~4000 K cool-white office/fluorescent; 5500-5600 K midday sun; ~6500-7500 K overcast; ~7000-8000 K open shade; 9000 K+ deep blue sky, blue hour.

Honest notes: real moonlight is ~4100 K, but viewers read cold blue as moonlight, so write "cold blue moonlight, about 8000 Kelvin". For deepest orange write about 1900 Kelvin.

## Light line template

```
LIGHT: [the source] only, about [2700 / 3200 / 5600 / 8000] Kelvin, from [direction]. It puts [the color, e.g. a warm orange-gold glow] on [the person]'s face, and [how the shadows fall]. No [colors not in the scene, e.g. daylight or blue light].
```

Four parts: the source, the number, what it does, what isn't there.

## Paste-ready light lines

**2700 K**
```
LIGHT: candlelight only, about 2700 Kelvin. [The candles in the scene] are the only light: a warm orange-gold glow that flickers on the faces and falls off to near-black within a few feet, with deep warm brown shadows. The flames are the brightest things in the frame, and there is no fill light. No blue light, no moonlight, no electric light.
```
Flicker comes from moving flames: describe them fluttering when someone moves. One background lamp or window ruins candlelight.

**3200 K**
```
LIGHT: [the lamp, e.g. a floor lamp with a pleated cream shade] is the only light, tungsten, about 3200 Kelvin: a steady, soft golden-amber glow, more yellow-gold and less orange than candlelight, with no flicker. It pools warmly on [the person] and [the nearest objects] and falls off softly into deep shadow. No daylight, no blue, no overhead or fluorescent light.
```
Candle vs tungsten: candle flickers, sits low, orange; tungsten is steady, higher, golden yellow.

**5600 K**
```
LIGHT: clean neutral midday sunlight, about 5600 Kelvin, high from [the left or right]. [The white things in the scene] read pure white with no yellow or blue cast, the colors are crisp and true, skin tones are real and natural, and the shadows are short, sharp and neutral gray. No golden-hour warmth, no blue tint, no haze.
```
White sheets/walls are the best daylight test.

**8000 K**
```
LIGHT: cold blue moonlight only, about 8000 Kelvin, from a full moon high on [the left or right]. It puts blue-white highlights on [the surfaces] and lights [the person]'s face a cool pale blue, the shadows are inky navy and the sky is deep blue-black, and [their breath steams in the cold air]. No warm light at all: no lamps, no fire, no warm glow on the skin.
```
Add cold evidence (breath, frost, snow) or blue reads as a filter. Rule out warm sources by name (torches, lanterns).

**Mixed warm inside / cold outside**
```
LIGHT: two colors of light. [The warm source, e.g. a tungsten table lamp], about [2700 or 3200] Kelvin, lights [the person]'s face from [direction] in warm amber, and it is the main light. Cold blue night through [the window], about 8000 Kelvin, edges [their shoulder and hair] from behind and fills the window with deep blue. The warm and the cold stay separate, and the shadows between them fall to near black. No daylight.
```
Give each light its own job; one is the main. Two equal lights from opposite sides make a face flat and muddy. When animating: "the lamplight stays steady and warm".

## WEAK → BETTER

WEAK: A woman walks home down a snowy street at night, cinematic lighting, moody, 8k.

BETTER: A woman walks home down a quiet snowy street of old houses at night, snow falling. The only light is cold blue moonlight, about 8000 Kelvin, from a full moon high on the right: blue-white highlights on the snow, navy shadows, her face lit a cool pale blue and her breath steaming. The sky is deep blue-black. No warm light, no street lamps, no daylight.

## Image template

```
Photorealistic [shot size] of [the person and what they are doing] in [the place, and the time of day], shot on a [35 / 50 / 85] mm lens at eye level. [Paste your light line]. [Two or three details of the place]. Real, unretouched skin, natural hands, no readable text, logos or signs.
```

Check whites at full size: 2700 K orange glow, 3200 K amber, 5600 K plain white, 8000 K pale blue.

## Fixes

| Problem | Change |
|---|---|
| Night still looks like day | Name the only source + number, "sky is deep blue-black", "no daylight", corners fall into shadow |
| Candle looks like a steady lamp | Flames flicker and are the only light, no fill, falls off to near black within a few feet |
| Midday comes out golden | "midday, sun high", short neutral shadows, "no golden-hour warmth", whites read pure white |
| Warm glow in a cold night | Rule out every warm source by name, "no warm glow on the skin" |
| Blue night too dark for faces | Moonlight lights the faces a cool pale blue |
| Everything tinted like a filter | Give the light a real source and direction; let shadows stay dark |
| Color changes between shots | Same light line word for word in every shot and take |

## Where it fails

- "At night" with no named source: the model lights it like day with a darker sky.
- One stray lamp or window in a candlelit scene breaks the candle look.
- Blue night with no cold evidence (breath, frost, snow) reads as a blue filter.
- A Kelvin number with no source next to it is a weak hint.
- Two lights of equal strength from opposite sides make the face flat and muddy.

<!-- Source: prompt-styles/references/color-temperature.md, distilled from PromptWise "The Color Temperature Cheat Sheet" (promptwise-free.vercel.app/22), fetched 2026-10-20. -->
