# Seedance (Seedance 1.x and Seedance 2.x)

| Version | Pick it for | Cost |
|---|---|---|
| Seedance 1.5 Pro, 1 Pro, 1 Lite | cheap single takes, short inserts (2 s on 1 Pro / 1 Lite), motion drafts | cheap |
| Seedance 2.0, 2.0 Fast | multi-shot in one clip, crowds, reference-heavy scenes (identity + motion video + music) | mid |
| Seedance 2.5 | the same, up to 30 s, more refs | premium |

Option names (duration, audio, resolution, mode, auto duration): check the provider's model
options.

## Shared formula (all versions)

`Subject + Action + Scene + Camera + Light/Style + Audio + Constraints`. Subject and main action
in the first clause.

| Slot | Pattern |
|---|---|
| Subject | `ceramic perfume bottle on black acrylic, label preserved exactly` |
| Action | `condensation beads form and slide down the glass over five seconds` |
| Scene | only what references don't show: `rain-lit kitchen counter, shallow depth of field` |
| Camera | one move with endpoint: `slow dolly-in from medium product shot to macro label detail` |
| Light/style | `warm practical key from frame left, cool blue rim, clean commercial realism` |
| Audio | `Sound: low room tone, soft glass chime on the final frame` |
| Constraints | `do not alter logo, shape, label or cap geometry` |

---

## Seedance 2.x (2.0, 2.0 Fast, 2.5)

**Model facts (at the time of writing; confirm in your provider):**
- Seedance 2.0: 480p to 4K (720p default on some providers); 4 to 15 s + auto; 1:1, 16:9,
  9:16, 4:3, 3:4; native audio. 1080p costs about 2.5x 720p on some providers: draft at 720p.
- Seedance 2.0 Fast: 480p and 720p only; otherwise the same; a little cheaper.
- Seedance 2.5: 480p to 1080p; 4 to 30 s + auto; adds an adaptive aspect; native audio; may
  offer a draft mode.
- References mode: up to 9 images, 3 videos, 3 audio clips (2.5: 30 / 10 / 10). Audio cannot be
  the only reference. Keyframes mode: first frame + last frame + video/audio refs. Video and audio
  refs 2 to 15 s each, 15 s total (2.5: 30 s). A video ref locks aspect to adaptive on 2.5.
- Audio on or off does not change the price on most providers.
- Realistic human faces in references may be refused. Use generated faces, not photos of real
  people.

### When to pick it

- **Use for:** multi-shot sequences in one clip, crowds and ensembles, reference-heavy scenes
  (identity + motion video + music), long clips on 2.5, motion transfer via a donor video.
- **Not for:** a single 2 s insert (4 s minimum), photo refs of real people.

### Compile

- **Slot order:** reference roles -> subject + action -> scene -> camera -> light/style ->
  audio -> constraints. Chronological.
- **Length:** 40 to 110 words per shot.
- **Timing / multi-shot:** label every cut `Shot 1:` `Shot 2:` ... about 4 to 6 s each (2 shots
  ~10 s, 3 shots 12 to 15 s). Per shot: one action + one move + its sound, in that order. End
  each shot on the completed beat. Timestamps ("at 5 seconds") are hints inside a labelled shot,
  not a replacement for labels. An auto duration option, if listed, suits multi-shot. One take:
  "single continuous take, no cuts". Persistent look declared once: "warm tungsten haze
  throughout, every shot".
- **References (model-native tags; syntax may differ by provider):** `@Image1..@Image9`,
  `@Video1..@Video3`, `@Audio1..@Audio3`, numbered per type in upload order. Always write the
  tag with its job ("follow @Video1 for camera movement only", "@Audio1 sets tempo only"). Keep
  tags literal (not `[Image1]`). Keep a plain-word echo "(image 1)" so the sentence still reads
  if the host maps references itself. If your provider describes references differently, use its
  wording and keep the same role discipline.
- **Audio:** name each shot's specific sounds; audio is made jointly with the picture, so named
  sounds anchor timing. Dialogue in quotes, in the shot where the speaker is on screen, short;
  lock framing (medium close-up, no head turn) for lip-sync.
- **When a reference carries it:** delete scene and identity description the refs already show;
  write only what does not transfer.

```
@Image1 (image 1) is the first frame. @Image2 (image 2) sets the boy's face and outfit only.
[Subject] [action with endpoint]. [Scene only if refs do not show it].
Camera: [one move with endpoint]. Light: [source]. [Look line].
Sound: [specific sounds tied to actions]   <- only if audio on
```

Role map template:
`@Image1 controls product identity. @Video1 controls camera pace only. @Audio1 controls tempo only. Do not copy people, logos, music or environment from @Video1 or @Audio1.`

#### Example

Bad (one ref doing four jobs, no labels):
> Use this image, kids cheering in the gym, then they jump, cinematic, dynamic, epic energy.

Good (keyframes mode, first frame given):
> @Image1 (image 1) is the first frame. About twenty schoolkids in matching yellow t-shirts press
> against the red ropes and scream, fists pumping; the girl in front pumps her hand-drawn
> cardboard sign "GO LEO!" up and down three times. Camera: kids' eye level, handheld, slow drift
> left along the ropes. Warm tungsten overheads, dust in the beams. 35mm film, soft grain.

Three-shot shape (~15 s):
> Shot 1: extreme close-up, condensation sliding down a glass bottle, ice clinking. Shot 2: the
> bottle rises from crushed ice, camera tilting up into a backlit halo. Shot 3: a hand grabs it
> against a sunset rooftop, the city humming below.

### Self-check

- [ ] Every tag has a stated job; tag numbering = reference list order per type
- [ ] 40 to 110 words per shot; shots labelled if more than one
- [ ] Duration fits shots x 4 to 6 s; at least 4 s
- [ ] Resolution chosen on purpose: 720p for drafts, 1080p for every clip in the final cut

### Failure modes

| Problem | Fix |
|---|---|
| Request refused | refs contain realistic real-person photos -> use generated stills |
| Long prompt renders as one take | label shots |
| Look flickers between shots | same look phrase every shot, or "throughout" once |
| Ref fights the prompt | delete re-description; add what does not transfer |
| Product or logo warps | "static identity, no shape change"; give it its own shot |
| 1080p bill shock | draft 720p; 1080p only for the final |
| Faces waxy or soft in the final edit | 720p upscaled to 1080p smooths skin, and faces soften later in a clip; final clips at 1080p, cut close-ups from the first 2-3 s, no extra scale push-in in the edit |

---

## Seedance 1.x (1.5 Pro, 1 Pro, 1 Lite)

**Model facts (at the time of writing; confirm in your provider):**
- Seedance 1.5 Pro: 480p to 1080p; 4 to 12 s + auto; 1:1, 16:9, 9:16, 4:3, 3:4; audio off by
  default on some providers; first + last frame. Cheapest of the family.
- Seedance 1 Pro: up to 1080p; 2 to 12 s; same aspects; first + last frame.
- Seedance 1 Lite: 480p and 720p; 2 to 12 s; first frame only.

### When to pick it

- **Use for:** cheap single-take shots, short inserts (2 s minimum on 1 Pro and 1 Lite), motion
  drafts, people shots when Seedance 2 refuses face refs.
- **Not for:** multi-shot, multi-reference, dialogue.

### Compile

- **Slot order:** subject + action -> scene -> camera -> light/style.
- **Length:** 30 to 80 words. One action, one move.
- **Timing:** none. No shot labels. Add "single continuous shot" if it cuts.
- **References:** first frame (and last frame on 1.5 Pro / 1 Pro). No tags.
- **Audio:** keep it out unless the provider offers it and the brief needs it.
- **When a reference carries it:** image to video = motion + camera + preserve line only.

```
[Subject or "the [role] in the image"] [action with endpoint]. Camera: [one move]. [Light]. [Look line].
```

#### Example

Bad: `Shot 1: ... Shot 2: ... @Image1 ...` (features it does not have)
Good: `The boy in the image grins wide, showing his missing front tooth, and raises his blue glove.
Camera: slow push-in from medium to close-up. Warm tungsten light. 35mm film.`

### Self-check

- [ ] One action, one move, 80 words or fewer
- [ ] Duration within the model's minimum (2 or 4 s)

### Failure modes

| Problem | Fix |
|---|---|
| Mushy action | one verb with a visible endpoint |
| Unwanted cut | "single continuous shot" |

---

## Field notes

### Pick the mode before writing

| Mode | Write | Common mistake |
|---|---|---|
| Text to video | the whole shot in compact layers | too many events in one clip |
| Image to video | only motion, camera, timing, light change, sound, locks | re-describing the image until the face or product drifts |
| Reference to video (several refs) | one role per reference + what must not transfer | one image asked to set identity, pose, scene and style |
| First + last frame | image 1 = first frame, image 2 = final target; describe only the transition | treating the last frame as "mood" |
| Video edit | "video 1 is the source; change only X" | rewriting the whole scene |
| Extend | continue from the observed last frame of the accepted clip | starting from the planned ending |

### Fast tiers

Fast tiers honour multi-shot, slow motion and dolly moves less reliably. Draft on 2.0 Fast,
final on Seedance 2.0.

### Image to video modes

- Template: `@Image1 is the reference; preserve [face/product/scene] exactly. Only [motion]
  changes. Camera: [one move]. Light: [source or transition]. Sound: [cue].`
- **Hold mode** (the image is the moment): 3 or 4 micro-actions (blink, breath, hair drift, slow
  gaze shift); lock the pose with a positive plus negative pair ("she stays seated; she does not
  stand or leave frame"); no move or one slow push-in.
- **React mode** (something happens): split the emotion into sub-beats with at least 2 s for the
  key beat. If the still is mid-action, add "the clip begins exactly at this moment".
- Drift: cut new description, strengthen locks. Output too still: add one physical action and
  one time cue. Hands deform: simplify hand motion.

### Motion transfer via references

Pair one donor video with one identity image and write the exclusion: `@Video1 controls the
choreography only; nothing of its performer, costume, room or logo transfers.` Choose donors with
one clear action, clean silhouette, steady camera. Transfers well: choreography, gesture timing,
camera rhythm. Transfers poorly: fine hands, multi-person sync, facial acting. For a dedicated
transfer model see video-edit-restyle.md.

### Audio across clips

Audio does not carry across separate runs: a multi-clip piece gets one score in the edit.

### Anti-slop

| Weak | Replace with |
|---|---|
| cinematic | shot size, move, light, grade |
| epic | physical scale, crowd size, lens distance |
| dynamic | the specific movement, speed, endpoint |
| dramatic | blocking, shadow, silence, camera pressure |
| cool transition | match cut, whip pan, dissolve, object wipe |
| magical | particle behaviour, glow source, path, interaction |
| 8K, masterpiece, trending | delete |

Rule: if a camera, microphone, light meter or stopwatch can't detect it, rewrite it.

### Fast diagnosis

| Problem | Lever |
|---|---|
| Generic despite long prompt | cut boosters, put priorities first |
| Excluded thing appears | describe the positive replacement |
| Action skipped or mushy | one cause, visible consequence, an endpoint |
| Identity decays across extensions | shorter clips, re-anchor on the original reference |
| Small detail breaks (logo, far face) | make it bigger in frame or give it its own shot |
| Lips or sound off | lock the face, shorten the line, name the sound |

Sources: RunDiffusion Seedance 2.0 guide (modes, @image1 roles, limits, face restriction);
Magichour reference guide; published Seedance docs as summarized by source skills; internal
production field notes.
