# FLUX 3 video (`flux_3`)

**Predis options:** `duration` int 5-20 + auto (default 5), `aspect` auto|21:9|2:1|16:9|4:3|1:1|3:4|9:16,
`resolution` 720p|1080p, `audio` (default true). first + last frame. 14 cr/s.

**Use for:** ultra-wide 21:9 / 2:1 establishing shots, long single shots up to 20 s with audio,
a FLUX-family look matching FLUX stills.
**Not for:** dialogue-critical shots (unproven), cheap drafts.

## Compile

No official video prompting guide found (2026-10-15). Use the FLUX image grammar plus video slots:
**subject first -> action with endpoint -> scene -> camera (one move) -> light -> style -> sound**.
40 to 120 words. Describe what you want; no negatives (FLUX family ignores them).

```
[Subject trait line] [action with endpoint] in [scene]. Camera: [one move from X to Y]. [Light].
[look_line]. Sound: [ambient], [effects].
```

- Hex colours tied to objects carry over from the FLUX image family: "gloves in hex #1F4FA0".
- With first + last frame: describe the transition only.

## Good vs bad
Bad: `epic wide landscape, no people, no birds, cinematic`
Good: `A lone red pickup drives along a straight desert road toward a storm wall at dusk. Camera:
slow aerial push forward from high wide to the truck's tail lights. Low amber sun from frame left,
dust trail glowing. Anamorphic 2.39 look, soft grain. Sound: wind, distant thunder.`

## Failure modes
| Symptom | Fix |
|---|---|
| Excluded thing appears | describe the replacement (empty sky), never "no X" |
| Unknown behaviour | draft at 720p, 5 s before a 20 s run |

## Self-check
- [ ] Subject first, no negations, one move
- [ ] Aspect chosen explicitly (default is auto)

Sources: describe_model; BFL FLUX.2 prompting guide (family grammar). Treat as provisional; log
what works in this file after the first runs.
