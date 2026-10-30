# Breakdown template

Fill every field you have evidence for. Write "inferred" when motion or intent is read from stills,
"unknown" when there is no evidence. Delete sections that do not apply. Label every audio claim:
measured, hint, transcript, user-said, or unknown.

````markdown
# <Title>: breakdown

**Source:** <file or link> · <duration>s · <W>x<H> (<aspect>) · <fps> fps · audio: yes/no
**Evidence:** frames (cuts / 1 fps / sheets / strips) · transcript: captions / WhisperX / whisper / none · sound: earshot / ffmpeg loudness only / none
**One-line read:** <what it is and why it works>

## Hook (0 to 3 s)
- What the viewer sees first:
- Why it stops the scroll:
- First words on screen / first sound:

## Pacing
- Shots: <n> · average shot length: <s>s · fastest stretch: <tc to tc>
- Cut rhythm: <on the beat (earshot: n of m cuts within <x> s of a beat) / on speech / irregular>
- Tempo: <bpm, measured / unknown>
- Structure: <hook, problem, demo, payoff, CTA, or story beats>

## Big moments
| Time | What happens on the frame | Audio at that time | Evidence |
|---|---|---|---|
| 4.0 | <action> | <hit, loudness jump, beat drop> | strip moment-4.0.jpg, earshot event |

## Layer map
| Layer | Present | Where (timecodes) | Rebuild with |
|---|---|---|---|
| Static background / plate | | | |
| Text overlay / captions | | | EDIT |
| Generated or filmed footage | | | |
| Screen recording / UI | | | user's own capture |
| Graphics / inserts | | | |
| Audio | | | |

## Look (whole piece)
- Palette and grade:
- Texture (grain, sharpness, phone vs cinema):
- Lighting style:
- Lens feel and depth of field:
- Typography (font feel, weight, colour, position, animation): EDIT
- Recurring motifs:

## Cast and sets
- <TAG>: <6 to 10 visible traits, reused word for word in every brief; no expressions here>
- <SET>: <set line>
- Look line: <one line pasted into every shot>

## Shot list
| # | In | Out | Shot / angle | Lens | Camera move (from -> to) | Subject + action | Setting | Light | Transition | On-screen text | Audio |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 0.0 | 1.8 | CU, eye level | 50mm, shallow | static | ... | ... | ... | hard cut | "..." (top centre) | ... |

## Beats
One line per moment, with the expression on that beat.
- 0.0 s: ...
- 1.2 s: ...

## Constraint per shot
- S<n>: <the one thing most likely to break -> how it must hold>

## Audio notes
- Source of evidence: <earshot sound pass + transcript / ffmpeg loudness and silence only>. I do not hear the audio myself.
- Loudness: <integrated LUFS (measured) / mean and max dB (measured)>. Silences at: <tc list>.
- Speech: <transcript with timecodes / "user says: ..." / unknown>
- Music: <sections with times (measured); mood or genre (hint) / user-described / unknown>
- Sound events: <time, level, tag (tag is a hint in a busy mix)>
- Sync to cuts: <which cuts land on hits or beats (measured)>

## Briefs
```yaml
cast: ...
set: ...
look_line: "..."
shots:
  - id: S1
    type: ...
    intent: "..."
    beat: "..."
    used_s: ...
    framing: {size: ..., angle: ..., placement: ..., must_be_in_frame: [...]}
    camera: {move: ..., from: ..., to: ..., speed: ...}
    lens: "..."
    motion:
      - {t: "0-0.8s", what: "..."}
    performance: "..."
    lighting: "..."
    style: look_line
    text_on_screen: none
    audio: {needed: ..., dialogue: [], ambience: ..., sfx: [], music: ...}
    references:
      - {ref: ..., role: ...}
    continuity: "..."
    avoid:
      - "<problem> -> <positive replacement>"
```

## Compiled prompts
Compiled per shot with `../model-router.md` and the matching `../models/<family>.md`.

### S1 to S3 · <model family> · <duration>s · <aspect> · refs: <list with roles>
```text
...
```

## Edit list
1. Clip S1-S3: 0.0 to 12.5
2. ...
3. Captions: <style, position, timing>
4. Music: <user file / native audio from clip X / none>
5. End card: <text, duration>
````

<!-- Adapted from MengTo/Skills video-to-superprompt (https://github.com/MengTo/Skills, MIT) -->
