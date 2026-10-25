# Grok Imagine Video (`grok_imagine_video_1_5`, `grok_video_extension`)

**Predis options:**
- `grok_imagine_video_1_5`: `resolution` 480p|720p|1080p, **`duration` int 1-15** (default 6),
  aspect 16:9|9:16|1:1|4:3|3:4|3:2|2:3. Ref modes: `keyframes` = first frame only; `references`
  = up to 7 images (**locks resolution to 720p**). No audio switch. 11 cr/s (3 s 34).
- `grok_video_extension`: v2v, needs a video. `duration` 2-10. 4 cr/s.

**Use for:** exact-length short inserts (1 s steps), stylized and bold looks, anime-like briefs,
extending an accepted clip.
**Not for:** realistic dialogue, complex multi-subject scenes.

## Compile

Order: **subject -> action -> mood/emotion -> setting -> light -> camera -> finishing style**.
30 to 90 words. Direct it like a filmmaker; emotional wording works here. Keep scenes simple.

```
[Subject] [action], [emotional tone]. [Setting], [light]. Camera: [named move: slow zoom in |
pan left | orbit]. [Style medium, plainly named: cel-shaded anime, flat shadows, bold outlines].
```

- Image-led: make the still first, animate with motion + camera only.
- Extension: "Continue: [what happens next from the observed last frame]. Camera keeps its
  [move]." Do not replay beats; re-anchor after 2 hops.
- Content-moderated? Describe the visual result, not the trigger subject.

## Good vs bad
Bad: `anime fight scene with 6 characters, lots of action, explosions, awesome`
Good: `A small boy in oversized blue gloves throws one tiny jab, proud and fierce. Old boxing gym,
warm overhead light. Camera: slow zoom in. Cel-shaded anime, flat shadows, bold outlines.`

## Failure modes

| Symptom | Fix |
|---|---|
| Multi-subject chaos | one subject, one action |
| Ref mode looks soft | references mode is capped at 720p; use keyframes for 1080p |
| Extension drifts | shorter hops; re-anchor on the original still |

## Self-check
- [ ] Duration = used_s + ~1.5 s (1 s steps available)
- [ ] One subject, one move, style named plainly

Sources: xAI-shared community guide (via Storyboard18/Basenor summaries), Puppetry Grok guide.
