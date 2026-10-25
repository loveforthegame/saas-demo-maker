# Director's Brief schema

One model-agnostic brief per shot. Fill it before you know the model. The compiler (one file per
model in `models/`) decides which fields become prompt words, which become config, and which are
dropped because a reference already carries them.

## 1. Cast bible (once per job)

```yaml
cast:
  MARCUS:
    trait_line: "a 6'6\" heavyweight boxer, shaved head, thick black beard, full sleeve tattoos on both arms, red satin shorts with gold trim, red boxing gloves, sweat sheen, kind eyes in a tough face"
    ref: A1            # reference image id/label once it exists
    voice: none        # or one concrete voice line, pasted word for word when they speak
  LEO:
    trait_line: "..."
    ref: A2
set:
  GYM:
    set_line: "old community boxing gym, worn blue ring canvas, red ropes, warm tungsten overhead lights, dust in the light beams, brick walls with faded fight posters"
    ref: A3
look_line: "35mm film, shallow depth of field, warm tungsten grade, soft film grain"
palette: ["#C8102E red gloves", "#1F4FA0 blue gloves", "#F2C230 yellow t-shirts"]   # tie each hex to an object
```

Rules: trait lines are 6 to 10 concrete, visible traits (age, build, hair, face marks, garment +
colour). Never names alone, never "same as before". The look line is pasted into every shot.

## 2. Shot brief

```yaml
- id: S6
  type: fast-action            # router key, see model-router.md
  priority: hero               # hero | support | filler  (drives tier + retake budget)
  intent: "the audience gasps then laughs: the giant is clearly faking it"   # a feeling, not an action
  beat: "Marcus throws himself backward and lands flat"                      # the ONE thing that changes
  used_s: 2.4                  # seconds the edit keeps
  gen_s: null                  # set at routing: min allowed >= used_s + 1.5
  aspect: "9:16"
  cast: [MARCUS, LEO]
  set: GYM
  framing:
    size: wide                 # extreme wide | wide | medium | medium close-up | close-up | extreme close-up | insert
    angle: "low, from the ring corner"   # eye level | low | high | overhead | POV | over-the-shoulder
    placement: "Marcus centre, Leo frame right, kids at the ropes behind"
    must_be_in_frame: ["Marcus full body", "Leo with glove out", "kids at the ropes"]
  camera:
    move: static               # one move: static | push-in | pull-out | pan | tilt | dolly | track | orbit | crane | handheld
    from: null                 # start framing when moving
    to: null                   # end framing when moving
    speed: null                # slow | medium | fast
  lens: "24mm, deep focus"
  motion:                      # timed beats; first one is the primary beat
    - t: "0-0.6s"
      what: "Marcus's whole body tips backward from the heels, arms flung wide"
    - t: "0.6-1.8s"
      what: "he travels through the air in slow motion, sweat drops spraying off his head into the light"
    - t: "1.8-2.4s"
      what: "his back lands flat on the canvas, a puff of dust lifts off the mat"   # endpoint
  performance: "Leo stays frozen, glove still out, mouth open"   # body-first cues, not emotion words
  lighting: "warm tungsten overheads from above, haze catching the beams"
  style: look_line             # or an override for this shot only
  text_on_screen: none         # exact words in quotes, or none (most text goes in the edit)
  audio:
    needed: false              # false = generate silent, sound in the edit
    dialogue: []               # [{speaker: MARCUS, line: "...", delivery: "low, amused"}]
    ambience: null
    sfx: []                    # [{at: "1.8s", sound: "body slams onto canvas"}]
    music: null                # or "no music"
  references:                  # order = reference_ids order = numbering in the prompt
    - {ref: B6, role: first_frame}
    - {ref: A1, role: identity, of: MARCUS, must_not_transfer: "background, pose"}
  continuity: "ends on Marcus flat on his back; S8 opens on the same pose from overhead"
  avoid:                       # each item = problem -> positive replacement
    - "real knockout -> the fall is big, slow and theatrical, arms flung wide like a stage dive"
    - "red gloves on Leo -> Leo's gloves are blue"
```

## 3. Field meanings the compiler relies on

| Field | Compiler uses it for | Dropped when |
|---|---|---|
| `intent` | framing choice, performance size; rarely literal words | never written as "the viewer feels X" |
| `beat` + `motion` | action sentence(s) and timing syntax | never |
| `framing` | shot size, angle, placement words | a first frame already fixes it (i2v) |
| `camera` | one move sentence with start and end | never; static still gets one line |
| `lens` | lens / DoF words | model ignores lens (drafts) |
| `cast.trait_line` | pasted verbatim | image ref carries identity AND model is weak with long text (keep a 3-trait anchor) |
| `set_line`, `lighting`, `look_line` | scene + light + style slots | first frame carries them (i2v): keep only light changes |
| `audio` | dialogue / SFX / ambience syntax, `audio` config | `needed: false` -> config audio off, no sound words except on models that invent sound |
| `references` | reference_ids order, ref mode, role sentences | never |
| `avoid` | positive statements; short constraint tail only where the model file allows | never written as "no X" on FLUX, Ideogram, MiniMax |

## 4. Shot `type` values (router keys)

`hero-still`, `character-sheet`, `text-graphic`, `vector-flat`, `product-still`, `draft-still`,
`establishing`, `character-performance`, `dialogue-lipsync`, `fast-action`, `crowd`,
`identity-locked-motion`, `multi-shot-sequence`, `product-motion`, `macro-texture`, `stylized-anime`,
`short-insert`, `long-take`, `restyle`, `extend`, `motion-transfer`.

## 5. Minimum viable brief (single image or quick clip)

For a one-off ask fill only: `type`, `intent`, `beat`, `framing.size`, `camera.move`, `lighting`,
`style`, `aspect`, `references`, `audio.needed`, `avoid`. Everything else defaults to "unspecified"
and the compiler skips the slot.
