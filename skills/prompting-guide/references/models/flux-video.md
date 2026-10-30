# FLUX 3 video

**Model facts (at the time of writing; confirm in your provider):** 5 to 20 s + auto (5 s default
on some providers); aspect auto, 21:9, 2:1, 16:9, 4:3, 1:1, 3:4, 9:16; 720p or 1080p; native audio
(on by default on some providers); first + last frame. Premium; priced per second.

Check the provider's model options for the exact parameter names (duration, aspect, resolution,
audio on/off, first/last frame).

## When to pick it

- **Use for:** ultra-wide 21:9 / 2:1 establishing shots, long single shots up to 20 s with audio,
  a FLUX-family look that matches FLUX stills.
- **Not for:** dialogue-critical shots (unproven), cheap drafts.

## Compile

No official video prompting guide was found at the time of writing. Use the FLUX image grammar
(see flux-image.md) plus video slots.

- **Slot order:** subject first -> action with endpoint -> scene -> camera (one move) -> light ->
  style -> sound.
- **Length:** 40 to 120 words.
- **Timing:** one continuous action with an endpoint.
- **Negatives:** none. Describe what you want; the FLUX family ignores negatives.
- **Colour:** hex colours tied to objects carry over from the FLUX image family: "gloves in hex
  #1F4FA0".
- **References:** first and last frame.
- **Audio:** a closing `Sound:` line with ambient and effects.
- **When a reference carries it:** with first + last frame, describe the transition only.
- **Aspect:** choose it explicitly; the default may be auto.

```
[Subject trait line] [action with endpoint] in [scene]. Camera: [one move from X to Y]. [Light].
[Look line]. Sound: [ambient], [effects].
```

### Example

Bad: `epic wide landscape, no people, no birds, cinematic`
Good: `A lone red pickup drives along a straight desert road toward a storm wall at dusk. Camera:
slow aerial push forward from high wide to the truck's tail lights. Low amber sun from frame left,
dust trail glowing. Anamorphic 2.39 look, soft grain. Sound: wind, distant thunder.`

## Self-check

- [ ] Subject first, no negations, one move
- [ ] Aspect chosen explicitly

## Failure modes

| Problem | Fix |
|---|---|
| Excluded thing appears | describe the replacement (empty sky), never "no X" |
| Unknown behaviour | draft at 720p, 5 s before a 20 s run |

## Field notes

Treat this file as provisional. Log what works here after the first real runs.

Sources: BFL FLUX.2 prompting guide (family grammar); model option listing at the time of writing.
