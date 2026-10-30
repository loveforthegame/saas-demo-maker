# Atmosphere: things to put in the air

Source: "4 Things to Put in the Air" (promptwise-free /25). For localized mist/fog/smoke/steam lines see [depth.md](depth.md).

Shots look like CGI when the air is perfectly clean: every distance equally crisp, light from nowhere. Fill the air, and **light it from behind**. Every air line has two halves: what is in the air + where the light is. The same haze or rain lit from the front almost vanishes.

## Cheat sheet

| Air | Words to paste | Where it fits |
|---|---|---|
| Haze | "thin haze, volumetric light, sun behind through the windows" | Factories, warehouses, churches, gyms, barns |
| Dust | "dust motes floating in a sunbeam, the sun behind" | Libraries, attics, barns, old houses, workshops |
| Embers | "sparks drifting past the face, backlit by the fire" | Campfires, bonfires, fire pits at dusk/night |
| Backlit rain | "rain lit from behind by headlights" | Night roads, a street under one lamp, any rain in the dark |

Why backlight: small particles scatter light mostly forward, so a source behind the air facing the camera glows brightest; and the camera-facing side is in shadow, so specks stand out against dark. Embers are the exception (self-lit), but they need a dark background; the fire behind backlights the person and sends sparks up past the face.

Vocabulary the model knows: Tyndall effect, god rays / crepuscular rays (need a strong light, something breaking it into beams, particles), volumetric light (pair with a real source), aerial perspective (far things paler, softer, bluer).

## Air lines

**Haze**
```
Thin haze, volumetric light, sun behind through the windows: the low sun shines through the windows toward the camera, and the thin haze turns it into crisp slanting shafts of light with dark gaps between them, while the person and the nearby objects stay clear and sharp.
```
Name what breaks the light (broken windows, skylight, blinds, doorway, trees). Shafts all run the same direction (sunlight is parallel).

**Dust**
```
Dust motes floating in a sunbeam, the sun behind: one slanting beam of warm sunlight comes through the window behind the person, and tiny dust motes drift and glint inside it, while the room around the beam stays dim.
```
In video give the dust a reason to move (blowing dust off a book, shaking a blanket, opening a door, walking through the beam).

**Embers**
```
Sparks drifting past the face, backlit by the fire: the fire a few steps behind the person is the main light and puts a warm, flickering orange rim on their hair and shoulders, and glowing embers rise on the hot air and drift up past their face against the dark sky.
```
Keep the fire contained and a few steps back (ring of stones, fire pit); sparks drift past, never land on skin. Say what is NOT burning ("an unburnt log in front, a separate fire behind"); filters may block scenes that look dangerous.

**Backlit rain**
```
Rain lit from behind by headlights: a car's headlights behind the person shine low toward the camera from a little to one side, so every falling drop shows as a bright white streak against the dark, the headlights put a bright rim on their hair and shoulders, and the wet ground shines.
```
Keep lights low and to one side (or let the person block one) so they don't flare out the frame; ask for a faint glow on the face. Wet ground, puddles, splashes sell it. Car: "no badges and no license plate".

## Image prompt pattern (dust example)

Photorealistic medium shot of a man in his fifties in a flannel shirt fixing an old motorbike inside a wooden barn on a summer afternoon, the camera facing the open barn door behind him. Dust motes floating in a sunbeam, the sun behind: bright sunlight pours in through the doorway and through the gaps between the wall boards, making slanting shafts full of glinting dust and specks of hay, and it puts a warm rim of light on his hair and shoulders. The inside of the barn stays dim, so the beams stand out, and his face is lit softly by light bounced off the straw on the floor. 35 mm lens. Real unretouched skin, natural hands with oil on the fingers, no readable text or logos.

(WEAK version it replaced: "...cinematic lighting, atmospheric, moody, 8k, ultra detailed, hyperrealistic.")

## Video prompt template

```
SET: [the place] [time], with [the light openings or source] and [details]. No readable text, signs or logos.
LIGHT AND AIR: [air line]. [The source] is the only strong light, [what it does in the air], [what it does to the person]. The [air] stays [thin / the same] for the whole shot.
SHOT: one continuous 5-second [SHOT SIZE], [lens] mm lens, [one camera move]: [your subject] [one action that interacts with the air].
SOUND: [the sounds]. No music.
LOOK: real [light] in real [air], with deep shadow [outside the beam / between the shafts]. Natural movement, real unretouched skin, hands with five fingers. No text, subtitles, logos or readable signs anywhere. No slow motion.
```

## Light position decides what you see

| Light from | Air does | Use for |
|---|---|---|
| Behind (facing camera) | Glows brightest, rim on person, face in shadow | Rain, embers, most drama |
| Behind, through gaps | Beams with dark gaps, parallel | Haze and dust in big rooms, forests |
| Side | Shafts cross frame, less glow | Beams across a room, half-lit faces |
| Front (behind camera) | Flat and gray; rain vanishes | Clear air on purpose, products |

- Hide the source (behind the person, window frame, tree, just outside frame).
- Keep the face readable with a clearly weaker second light (ground bounce, side window, fire glow).
- One main air per shot; anything else thin.
- Same air line in every shot.

## Air line template

```
[The air] [where it is], lit from behind by [the light source], which sits [where] and faces the camera, so [what it does in the air] and [what it does to the person]. The background stays dark, [the face or the main detail] stays clear, and there is no light from the front.
```

More air: snow (backlit flakes glow), mist over water at sunrise, steam against dark with light behind, smoke curls, sea/waterfall spray (rainbow if sun behind camera), pollen/seed fluff in low golden backlight.

## Where each struggles

- **Haze**: lifts blacks, too much = milky flat frame; useless in front light/overcast; bad for product crispness. Write "thin" and what stays sharp.
- **Dust**: needs a dim room and one hard beam; overdone = snow/glitter/bokeh balls. "Tiny, fine motes that show only inside the beam."
- **Embers**: vanish in daylight; overdone = fireworks or falling. "A few dozen drifting up"; fire visible or clearly behind.
- **Rain**: vanishes in daylight/front light; on-camera flash = blurry dots; overdone = straight even white lines. Video models may slow it or leave people dry: "rain falling at real speed, wet hair and a wet coat, no slow motion".

## Fixes

| Problem | Change |
|---|---|
| Air looks empty | Name air + light position, source behind facing camera, remove 8k/ultra detailed/hyper sharp |
| Frame milky gray | "thin haze", person and nearby objects clear, dark parts stay dark |
| God rays fan out | One source, shafts run parallel to bright patches on the floor |
| Dust looks like snow/glitter | Tiny fine motes only inside the beam, room dim |
| Wrong thing on fire | Fire separate, contained, a few steps behind; name what isn't burning |
| Sparks look like fireworks | A few dozen embers drifting up, dark sky, don't touch the person |
| Rain barely shows | Light behind facing camera, dark background, each drop a bright streak |
| Headlights wash out frame | Low and to one side, or person blocks one; faint glow on face |
| Air fades in video | Still as first frame; "stays the same for the whole shot" |

<!-- Source: prompt-styles/references/atmosphere.md, distilled from PromptWise "4 Things to Put in the Air" (promptwise-free.vercel.app/25), fetched 2026-10-20. -->
