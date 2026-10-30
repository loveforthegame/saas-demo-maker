# Aperture and focus

Source: "The Aperture Cheat Sheet" (promptwise-free /18).

Low f-number = wide opening = shallow depth of field. High = small opening = deep focus. Depth of field also depends on focal length and camera distance, so always pair the f-stop with a lens and a distance. In prompts the f-stop is a focus instruction; set brightness by describing the light.

## Pick the look

| F-stop | Look | Use for | Pair with |
|---|---|---|---|
| f/1.4 | Only the eyes sharp, round bokeh behind | Close-ups, night scenes | 85 mm, 1 m from face |
| f/2.8 | Subject pops, room still readable | People at work, products, interviews | 50 mm, 2-3 m away |
| f/8 | Sharp front to back | Streets, groups, travel | 35 mm, 5 m+ away |
| f/16 | Sharp to the horizon | Scenery, big views, architecture | 24 mm, horizon in frame |

In between: f/2, f/4, f/5.6, f/11 each deepen focus a little.

## Lens blocks

**f/1.4**
```
Shot on an 85 mm lens at f/1.4, the camera about one meter from [the subject]'s face. Razor-thin focus on [the eyes], with the ears and hair already slightly soft. [The lights behind them] melt into large, soft, round circles of light with no readable detail.
```
Keep action small (glance, breath); movement toward/away slides out of focus. For video add "the focus stays on her eyes for the whole shot".

**f/2.8**
```
Shot on a 50 mm lens at f/2.8, the camera about two and a half meters from [the subject]. [The subject] is sharp from head to hands, and [the room behind them] is softly blurred but still easy to recognize.
```
Two people at different distances may not both be sharp: keep them side by side or name the focus target.

**f/8**
```
Shot on a 35 mm lens at f/8 with deep focus, the camera about five meters from [the subject]. Everything is sharp, from [the nearest detail] at the front of the frame to [the farthest detail] behind, with no background blur.
```
Models add background blur by habit: name the far details that must stay sharp. For a moving subject, camera keeps the same distance (walks backward with them).

**f/16**
```
Shot on a 24 mm lens at f/16 with deep focus. Everything is sharp, from [the nearest detail] to [the far horizon], with crisp detail in the far distance and no background blur.
```
Thin haze is fine (lowers contrast, not focus); heavy haze reads as soft.

## Background wording by f-stop

| F-stop | Describe the background as |
|---|---|
| f/1.4 | "melt into large, soft, round circles of light with no readable detail" |
| f/2.8 | "are softly blurred but still easy to recognize" |
| f/8 | "stay sharp and readable from the front of the frame to the back" |
| f/16 | "are sharp all the way to the horizon, with crisp detail in the far distance" |

## Three habits

1. **Number + result**: f-stop, then what is sharp and what is soft.
2. **Give bokeh something to blur**: small bright points behind (lanterns, string lights, street lamps, candles, sun through leaves). A plain wall becomes a flat wash.
3. **One focus target**: name exactly one sharp thing; place everything else relative to it.

Avoid mixed messages: "f/1.4, everything razor sharp to the street outside" makes the model pick one.

## WEAK → BETTER

WEAK: A woman eating ramen at a bar at night, cinematic, shallow depth of field, blurry background.

BETTER: Close-up of a woman at a ramen counter at night, 85 mm lens at f/1.4, the camera about one meter from her face. The focus is on her eyes, and her ears are already slightly soft. The paper lanterns and neon behind her melt into large, soft, round circles of light.

## Rack focus (video)

Needs f/1.4 or f/2.8, two targets at clearly different distances, a time, a locked-off camera.

```
... one continuous shot with a locked-off camera. A steaming bowl sits on the counter close to the lens, and a young woman sits behind it, about a meter farther back. Shot on a 50 mm lens at f/1.4. For the first two seconds the focus is on the bowl and the rising steam, and she is a soft shape behind it. Then she looks up, and the focus pulls smoothly from the bowl to her eyes over about one second; the bowl goes soft, and her face becomes sharp and stays sharp to the end. The paper lanterns behind her stay as soft round bokeh throughout.
```
Expect several takes.

## Fill-in template

```
[Shot size] of [subject] [doing one simple action] in [location], [time of day and light]. Shot on a [focal length] lens at [f-stop], the camera about [distance] from [subject]. The focus is on [one focus target], [what else is sharp or slightly soft]. Behind them, [background details] [background wording from the table]. The camera [one simple movement].
```

Image-first: generate the still, check focus, use as first frame, keep only action/camera/sound lines and add "Keep the focus exactly as it is in the image."

## Fixes

| Problem | Change |
|---|---|
| Background sharp at f/1.4 | Closer camera, 85 mm, more subject-to-background distance, describe round circles of light |
| Face as soft as background | One focus target + "focus stays on it for the whole shot" |
| Background blurs at f/16 | Delete "shallow depth of field"/"bokeh"/"cinematic blur" from style lines, wider lens, list far details |
| Far distance soft at f/16 | Thin out the haze or mist |
| Bokeh is a flat smear | Add small light sources behind |
| Focus wanders in video | Start from a still, small action, "keep the focus on her eyes for the whole shot" |
| Rack focus never happens | Start target, end target, time, different distances, still camera |

## Where it fails

- f/1.4 with a moving subject: movement toward or away from the lens slides out of focus.
- f/2.8 with two people at different distances: only one is sharp unless they stand side by side or the focus target is named.
- f/8 and f/16: models add background blur by habit unless far details are named as sharp.
- A plain wall behind the subject gives no bokeh, only a flat wash.
- Mixed messages ("f/1.4, everything razor sharp") make the model pick one.

<!-- Source: prompt-styles/references/aperture.md, distilled from PromptWise "The Aperture Cheat Sheet" (promptwise-free.vercel.app/18), fetched 2026-10-20. -->
