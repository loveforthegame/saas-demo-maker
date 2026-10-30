# Kling (Kling 2.x, Kling 3, Kling O3 Pro, Kling 3 Omni)

One family, three prompt styles. Pick the version first, then read its subsection.

| Version | Pick it for | Cost |
|---|---|---|
| Kling 2.x (2.6, 2.5 Turbo, 2.1) | cheap motion drafts of a Kling 3 shot; animate-a-still | cheap |
| Kling 3 (Pro, Standard) | bodies with weight, contact, stunts; A-to-B arcs; dialogue when Veo is not an option | mid to premium |
| Kling O3 Pro | the same character across shots: first frame + identity refs in one call; 3 s shots | mid |
| Kling 3 Omni | reference-driven scenes (images + a video); editing a clip while adding a referenced object | premium |

Exact option names (start image, end image, duration, audio, mode, multi-shot / storyboard)
differ per version and per provider: check the provider's model options before every first use.
Do not promise native audio unless the provider lists it for that version.

## Shared rules (all versions)

- One primary camera move per shot, written with a start and an end ("crane up from the wet
  street to a wide of the skyline"), or "Camera: static, on a tripod".
- Physical cause and consequence beats stage directions: "the wave hits the pier, spray bursts
  over the railing" rather than a list of micro-moves.
- Image to video: the start image is the first frame. Prompt motion, camera and change over
  time only. Lock what must hold: "preserve face, outfit and room layout; only the curtains and
  her hair move in the breeze". Never re-describe the image.
- First + last frame: describe only the transition, and make the last frame the physical end
  state (seated, landed, closed). Example: "the room fills with morning light as the camera
  pushes toward the window".
- Never write "no static" or put "static" in an avoid list: it kills camera motion. State the
  move instead.

---

## Kling 3 (Pro, Standard)

**Model facts (at the time of writing; confirm in your provider):** 5 to 10 s; 16:9, 9:16, 1:1;
first + last frame; native audio (on by default on some providers). No resolution choice.
Image refs at least 300 px, aspect no more extreme than 2.5:1. Audio off is about a third cheaper
on some providers; check your provider's price.

### When to pick it

- **Use for:** bodies with weight, contact, falls, stunts, lifts; controlled A-to-B arcs with a
  last frame; dialogue scenes when Veo is not an option (native audio, multi-language).
- **Not for:** shots that truly need under 5 s (minimum 5), identity from several refs (Kling O3).

### Compile

- **Slot order:** subject (trait line) -> action with cause and consequence -> setting -> camera
  -> light -> style -> audio.
- **Length:** 50 to 120 words for one shot; up to about 6 labelled shots in one clip.
- **Film language:** Kling reads "tracking shot", "profile shot", "macro close-up", "POV",
  "shot-reverse-shot". Use it, one move per shot.
- **Timing / multi-shot:** a one-line master description of the subjects first, then
  `Shot 1 (0-4s): ...` `Shot 2 (4-8s): ...`, each with framing, subject, motion. About 4 to 6 s
  per shot. Subject description identical in every shot. If the provider exposes a dedicated
  multi-shot or storyboard option, use it instead of prose labels.
- **References:** first frame = anchor; last frame = end state. No identity-ref slot (use O3).
- **Audio / dialogue:** label speakers with a bracketed, unique descriptor including voice:
  `[Black-suited agent, raspy deep voice]: "..."`. Put the physical action before the line.
  Use "Immediately," when the speaker switches. Never "he says".
  Sound added in the edit: switch audio off in the provider and write no sound words.
- **When a reference carries it:** with a first frame, drop the trait line and write a preserve
  line instead.

```
[Subject trait line] [action, written as cause -> visible consequence -> endpoint]. [Setting].
Camera: [shot size], [one move from X to Y, speed]. Light: [sources]. Style: [look line].
```

#### Example

Bad (first frame re-described, two moves, no endpoint):
> A huge boxer with a beard and tattoos in a gym falls down dramatically, camera zooms and pans
> around, epic cinematic slow motion.

Good (image to video, first frame = boxer upright after the jab):
> The giant boxer throws himself backward from his heels, arms flung wide like a stage dive, sails
> through the air in slow motion with sweat drops spraying into the light, and lands flat on his
> back on the blue canvas, a puff of dust lifting off the mat. The small boy stays frozen with his
> blue glove still out. Camera: wide, static, low angle from the ring corner. Preserve both faces,
> outfits and the gym exactly.

### Self-check

- [ ] Trait line verbatim (text to video) or a preserve line (image to video)
- [ ] Action written as cause -> consequence -> endpoint
- [ ] One camera line; duration 5 to 10 s; audio setting matches the brief
- [ ] Last frame given whenever the end state matters

### Failure modes

| Problem | Fix |
|---|---|
| Camera wanders | one move with start and end, or "Camera: static, on a tripod" |
| Face drifts from the first frame | delete re-description; add "preserve faces and outfits" |
| Motion too timid | one bigger physical action with a visible result |
| Plug, key or lid never seats, or is the wrong size | name the real part sized to its mate; make start + end keyframes (end = seated) and pass them as first and last frame |
| Warped hands or product | simplify the hand action; keep the product static and named |
| Speakers merge | bracketed unique labels, action before line, "Immediately," at switches |
| Paying for audio you will replace | switch audio off |

---

## Kling 2.x (2.6, 2.5 Turbo, 2.1)

**Model facts (at the time of writing; confirm in your provider):**
- Kling 2.6: 5 or 10 s; 16:9, 9:16, 1:1; native audio; first frame only. Mid cost.
- Kling 2.5 Turbo: 5 or 10 s; 16:9, 9:16, 1:1; first frame only. Cheap.
- Kling 2.1: image to video only (needs an image); standard or pro mode; 5 or 10 s; first + last
  frame. Cheap.

### When to pick it

- **Use for:** cheap motion drafts of a Kling 3 shot (Turbo), cheap animate-a-still with an end
  state (2.1 first + last), aggressive camera moves (Turbo follows "fast drone follow",
  "whip pan").
- **Not for:** dialogue, multi-shot, identity across many refs.

### Compile

- **Slot order:** subject -> action -> camera -> environment -> style.
- **Length:** 30 to 80 words. Shorter than Kling 3; one action, one move.
- **Timing:** none; one beat per clip.
- **References:** first frame (2.1 also last frame).
- **Audio:** 2.6 only; not for dialogue.
- **When a reference carries it:** image to video = motion + camera + "preserve face and outfit";
  nothing else.
- **Promote a Turbo draft to Kling 3 Pro:** keep the prompt, add the full trait line and light.

```
[Subject, 3-5 traits or "the [role] in the image"] [one action with endpoint]. Camera: [one move].
[Setting only if text to video]. [Look line].
```

#### Example

Bad: `boxer falling, dramatic, slow motion, 8k, masterpiece`
Good: `The boxer in the image tips backward and falls flat onto the canvas in slow motion, arms
wide. Camera: static wide. Preserve his face, beard and red gloves.`

### Self-check

- [ ] 80 words or fewer, one action, one move
- [ ] Duration is 5 or 10
- [ ] Kling 2.1 has an image

### Failure modes

| Problem | Fix |
|---|---|
| Static output | stronger verb, a visible result, a speed word |
| Jitter or melting on 10 s | use 5 s; split the action |
| "static" in an avoid list kills camera motion | never write "no static"; state the move |

---

## Kling O3 Pro and Kling 3 Omni

**Model facts (at the time of writing; confirm in your provider):**
- Kling O3 Pro: 3 to 15 s; 16:9, 9:16, 1:1; native audio. Combined mode: 1 first frame + up to
  4 reference images in one call. Duration scales price linearly, so a 3 s shot costs about 60 %
  of a 5 s one. Audio off is cheaper on some providers.
- Kling 3 Omni: standard or pro mode; 3 to 15 s; 16:9, 9:16, 1:1; audio off by default on some
  providers. Up to 7 images + 1 video as references. Also video to video (edit a clip with refs).
  Premium.
- Image refs at least 300 px, aspect no more extreme than 2.5:1.

### When to pick it

- **Use for:** the same character across many shots (first frame + identity refs in one call),
  short shots (3 s minimum), reference-driven scenes, editing a clip while adding a referenced
  object (Omni).
- **Not for:** heavy physics stunts (Kling 3 Pro), dialogue-led hero shots (Veo).

### Compile

- **Slot order:** reference roles -> action -> environment -> camera -> light -> style.
- **Length:** 40 to 100 words.
- **Timing:** one beat; 3 to 5 s is enough. Choose duration as seconds used in the edit + 1.5 s.
- **References:** refer by position in the reference list: "image 1", "image 2". For safety
  across hosts, add the tag form in brackets once: "the boxer (@Image2)". Element syntax varies
  by host; keep the prose readable without the tag.
  - O3 is optimized for 1 to 2 identity references. Four is the ceiling, not the target.
  - Give each ref one job (identity, outfit, product, set) and say what must not transfer
    ("only the face from image 2, not its background or pose").
  - Order: first frame first in the reference list, then refs in prompt order.
- **Audio:** set on or off to match the brief.
- **When a reference carries it:** with a first frame, never re-describe it; describe what
  moves. Omni with a video ref: "Video 1 is the source; keep its timing and camera; change
  only ...". For pure restyles on Omni see video-edit-restyle.md.

```
Image 1 is the first frame. The [role] from image 2 and the [role] from image 3 keep their faces
and outfits exactly. [Action with endpoint]. Camera: [one move]. Light: [only changes]. [Look line].
```

#### Example

Bad:
> Make a video with these images of the boxer and the kid in the gym doing boxing.

Good (first frame + one identity ref):
> Image 1 is the first frame. The boy from image 2 keeps his face, freckles and missing front
> tooth exactly. He draws one deep breath that lifts his small shoulders; the oversized blue
> headgear slides down over one eyebrow; he pushes it back up with his blue glove and frowns
> harder. Camera: close-up, static, slight handheld drift. 35mm film, warm tungsten, soft grain.

### Self-check

- [ ] First frame first in the reference list, then refs in prompt order
- [ ] Each ref has one role + a "not" clause
- [ ] Duration = seconds used + 1.5 (3 s is allowed)
- [ ] Audio setting matches the brief

### Failure modes

| Problem | Fix |
|---|---|
| Two copies of one person | state headcount: "exactly two people: the boxer and the boy"; fewer refs per person |
| Ref background leaks into the shot | "take only the face and outfit from image 2" |
| Wrong ref used for wrong role | reference list order must match the prompt numbering |
| Stiff motion | one bigger body action; 3 to 5 s is enough |

## Field notes

- Drafting path: draft on Kling 2.5 Turbo, lock the look, then re-run on Kling 3 Pro or Kling 3
  Standard.
- Kling 3 multi-shot: label shots, one action and one move each, about 4 to 6 s per shot, the
  character line repeated in every shot.
- Kling 3 is the most reliable family member with bodies, weight and contact; use it as the
  default for fast action.

Sources: fal.ai Kling 3.0 prompting guide; VEED and Artlist Kling 2.5 Turbo guides; Hedra model
page; Kling blog "V3 vs O3" (1-2 elements optimal); Runware/Opper O3 docs (element syntax varies
by host); internal production field notes.
