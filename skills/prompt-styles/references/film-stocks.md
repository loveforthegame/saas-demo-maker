# Film stocks

Source: "5 Film Stocks for Your Prompts" (promptwise-free /24).

With no camera or film named, the model defaults to clean, sharp, evenly lit digital (phone) footage. Write the film's full name + "shot on 35mm film" + look words. If the model doesn't know the name, the look words still carry it. The model imitates the look from captioned photos; it is not a true emulation.

## Cheat sheet

| Stock | Type | Look | Use for | Best light | Lens |
|---|---|---|---|---|---|
| Kodak Gold 200 | Color neg, ISO 200, daylight | Warm golden-yellow cast, saturated reds/yellows, fine grain | 90s summers, family photos | Hard midday sun or direct flash | 35 mm, all in focus |
| Kodak Portra 400 | Color neg, ISO 400, daylight | Warm natural skin, soft pastels, low contrast, fine grain | Weddings, portraits | Soft backlight, open shade, window | 85 mm f/2 |
| Fujifilm Velvia 50 | Color slide, ISO 50, daylight | Hugely saturated, deep blues/greens, rich contrast | Postcard landscapes | Clear low sun, deep blue sky | 24 mm f/11 |
| Ilford HP5 Plus | B&W neg, ISO 400 | B&W only; pushed: deep blacks, gritty grain | Detectives, moody | One hard light (blinds, street lamp) | 35/50 mm handheld |
| CineStill 800T | Color neg, ISO 800, tungsten | Cool teal shadows, red halation around lights, visible grain | Neon, night streets | Neon, lamps, street lights at night | 35 mm f/1.4 bokeh |

## Film lines (paste verbatim)

**Gold 200**
```
Shot on Kodak Gold 200, 35mm film: a warm golden-yellow cast, saturated reds and yellows, soft creamy highlights and fine visible grain, like a 1990s family snapshot.
```

**Portra 400**
```
Shot on Kodak Portra 400, 35mm film: warm, natural, flattering skin tones, soft pastel colors, low contrast, creamy highlights and fine grain.
```
Airier: add "slightly overexposed, bright and airy".

**Velvia 50**
```
Shot on Fujifilm Velvia 50, 35mm slide film: hugely saturated color, deep blues and greens, rich contrast and very fine grain, crisp like a postcard.
```
Name the strong colors in the scene.

**HP5 Plus**
```
Shot on Ilford HP5 Plus, 35mm black-and-white film pushed to 1600: black and white only, no color at all, deep blacks, bright highlights and strong, gritty grain.
```
Drop "pushed to 1600" for gentler; "pushed to 3200" for more grit.

**CineStill 800T**
```
Shot on CineStill 800T, 35mm film: tungsten-balanced, cool teal shadows, a soft red halation glow around the brightest lights only, visible grain.
```

## Stock tips

- **Gold**: date the picture with props from the decade (inflatable pool, camcorder, station wagon).
- **Velvia**: it exaggerates colors already present, so put strong colors in front of the camera.
- **HP5**: say "black and white" in the film line, the shot and the look; models drift to sepia/blue or back to color.
- **CineStill**: ask for bare neon tubes bent into loops and lines, "no letters or symbols anywhere" (signs get fake letters).

## Where each struggles

- **Gold**: fights cold scenes (snow, blue night, white studio); skin can go orange; bad for true-color product shots; weak in the dark without flash.
- **Portra**: bold scenes look tame and flat (use Velvia); not for neon nights (use CineStill); no thriller contrast.
- **Velvia**: pushes skin red (keep people small or use Portra); harsh midday shadows go black; bad for soft moods or dim light.
- **HP5**: no use when color is the point (food, fashion, product); makes cheerful scenes heavy.
- **CineStill**: turns blue in daylight; halation can overrun into a red haze, so "around the brightest lights only".

## Image prompt template

```
Photorealistic [shot size] of [your subject] [doing what] in [the place, at what time of day]. [The light: its source, direction and color]. [24 / 35 / 50 / 85] mm lens at [f/1.4 / f/2 / f/8 / f/11], [what stays in focus]. Shot on [the film stock], 35mm film: [the look words from the cheat sheet]. Real unretouched skin, natural hands, no readable text or logos.
```

## Video prompt template

```
SET: [the place] [time], with [one or two details]. No readable text or logos.
LIGHT: [the light that suits the stock].
FILM: the look of [stock] 35mm film, 24 frames per second: [look words].
SHOT: one continuous 5-second [SHOT SIZE], [lens] mm lens, [one camera move]: [your subject] [one action].
SOUND: [the sounds]. No music.
LOOK: real [stock] 35mm film texture throughout. Natural movement, real unretouched skin, hands with five fingers. No text, subtitles, logos or readable signs anywhere. No slow motion.
```

"35mm film" is film size; "35mm lens" is focal length. Both can sit in one prompt; for a tight portrait on 35mm film write an 85mm lens.

## Pairings to try

- Gold 200 + direct on-camera flash at night = 90s party snapshot.
- Portra 400 + cloudy day = soft even skin for close portraits.
- Velvia 50 + golden hour = postcard sunset.
- HP5 Plus + single street lamp in rain = film noir.
- CineStill 800T + headlights on a wet road = red glow on every light and reflection.

One film per scene, same line in every shot. Deliberate switches work (Gold 200 flashback inside a Portra 400 present).

## WEAK → BETTER

WEAK: A family having a barbecue in the backyard, vintage film look, retro filter, nostalgic, cinematic, 8k, ultra detailed.

BETTER: Photorealistic snapshot of a family barbecue in a 1990s backyard on a hot summer afternoon: a dad flips burgers at a red kettle grill while two kids run through a lawn sprinkler behind him. Hard bright sun and sparkling water drops. Shot on Kodak Gold 200, 35mm film: a warm golden-yellow cast, saturated reds and greens, soft creamy highlights and fine visible grain, like a print from a family photo album. Real unretouched skin, natural hands, no readable text or logos.

## Fixes

| Problem | Change |
|---|---|
| Looks like a filter | Remove vintage/retro/filter/faded; keep name + look words; describe a real light |
| Still clean and digital | Name + "35mm film" + grain phrase; remove 4k/8k/ultra detailed/hyper sharp |
| Model ignores the name | Check spelling/number; lean on look words |
| Skin orange or red | "natural skin tones", or switch to Portra 400 |
| B&W comes out tinted | "black and white only, no color, no sepia, no tint" in film line and at end |
| Red glow over whole frame | "a soft red halation glow only around the brightest lights" |
| Neon has fake letters | Bare tubes, "no letters, characters or symbols anywhere" |
| Video loses the film look | Still first as first frame, keep film line, end with "real film texture throughout" |
