# Grok Imagine Video (Grok Imagine Video 1.5, Grok Video Extension)

**Model facts (at the time of writing; confirm in your provider):**
- Grok Imagine Video 1.5: 480p to 1080p; **1 to 15 s in 1 s steps** (6 s default on some
  providers); 16:9, 9:16, 1:1, 4:3, 3:4, 3:2, 2:3. Keyframes mode = first frame only; references
  mode = up to 7 images (**locks resolution to 720p**). No audio switch. Mid cost.
- Grok Video Extension: video to video, needs a source clip; 2 to 10 s added. Cheap.

Check the provider's model options for the exact parameter names (duration, resolution, first
frame, reference slots).

## When to pick it

- **Use for:** exact-length short inserts (1 s steps), stylized and bold looks, anime-like briefs,
  extending an accepted clip.
- **Not for:** realistic dialogue, complex multi-subject scenes.

## Compile

- **Slot order:** subject -> action -> mood/emotion -> setting -> light -> camera -> finishing
  style.
- **Length:** 30 to 90 words. Direct it like a filmmaker; emotional wording works here. Keep
  scenes simple: one subject, one action.
- **Timing:** none inside the clip; set the exact length instead (seconds used in the edit +
  about 1.5 s).
- **Camera:** a named move: "slow zoom in", "pan left", "orbit".
- **Style:** name the medium plainly: "cel-shaded anime, flat shadows, bold outlines".
- **References:** up to 7 images (720p cap); for 1080p use a first frame instead.
- **Audio:** no switch; plan sound in the edit.
- **When a reference carries it:** image-led, make the still first and animate with motion +
  camera only.
- **Extension:** "Continue: [what happens next from the observed last frame]. Camera keeps its
  [move]." Do not replay beats; re-anchor after 2 hops (details in video-edit-restyle.md).
- **Moderation:** if a prompt is blocked, describe the visual result, not the trigger subject.

```
[Subject] [action], [emotional tone]. [Setting], [light]. Camera: [named move: slow zoom in |
pan left | orbit]. [Style medium, plainly named: cel-shaded anime, flat shadows, bold outlines].
```

### Example

Bad: `anime fight scene with 6 characters, lots of action, explosions, awesome`
Good: `A small boy in oversized blue gloves throws one tiny jab, proud and fierce. Old boxing gym,
warm overhead light. Camera: slow zoom in. Cel-shaded anime, flat shadows, bold outlines.`

## Self-check

- [ ] Duration = seconds used + about 1.5 s (1 s steps available)
- [ ] One subject, one move, style named plainly

## Failure modes

| Problem | Fix |
|---|---|
| Multi-subject chaos | one subject, one action |
| Reference mode looks soft | references mode is capped at 720p; use a first frame for 1080p |
| Extension drifts | shorter hops; re-anchor on the original still |
| Near-identical takes | vary the prompt wording |

## Field notes

Stylized briefs (anime-like, high-contrast, bold colour) are where this model earns its place.
Name the medium plainly rather than with adjectives.

Sources: xAI-shared community guide (via Storyboard18/Basenor summaries); Puppetry Grok guide;
internal production field notes.
