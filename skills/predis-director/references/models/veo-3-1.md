# Veo 3.1 (`veo_3_1`, `veo_3_1_fast`)

**Predis options (describe_model 2026-10-15):** `resolution` 720p|1080p|4K (default 1080p),
`duration` 4|6|8 (default 8), `aspect` 16:9|9:16, `audio` bool (default true). Ref modes:
`references` = up to 3 images (identity/style "ingredients"), **locks duration to 8**;
`keyframes` = first_frame + last_frame. 21 cr/s (fast: 6 cr/s); audio does not change price.

**Use for:** dialogue with lip-sync, shots where sound sells it, macro and light. Draft on
`veo_3_1_fast`, final on `veo_3_1` with the identical prompt.
**Not for:** 1:1 or 4:5, shots over 8 s, cheap filler.

## Compile

Order: **camera -> subject -> action -> setting -> light -> style -> audio block**.
Length: 80 to 180 words. Veo rewards dense, concrete prose; it does not reward adjectives.

```
[Shot size], [angle], [one camera move with start and end]. [Subject trait line] [action with
endpoint], [setting from set_line]. [Light sources]. [look_line].
Dialogue: [Speaker tag] says: "[line]" ([delivery]).
SFX: [sound] as [action]. Ambient noise: [place sound]. Music: [genre/mood or "none"].
(no subtitles)
```

- Timing for 2 to 3 beats inside one clip: timestamp brackets `[00:00-00:02] ... [00:02-00:05] ...`.
  More than 3 beats in 8 s: split the shot.
- Dialogue: 2 to 3 short sentences per 8 s max. Speaker by visual tag, never a pronoun. Quotes
  plus a colon trigger speech; without them the words can render as on-screen text.
- `audio.needed: false`: set `audio=false` and omit the audio block (price is the same either way,
  so consider keeping audio as a free scratch track).
- Keyframes mode: the prompt describes only the motion and sound between the frames.
- References mode: say each ingredient's job ("the man from image 1, the jacket from image 2").
  Remember duration becomes 8.
- Avoid list: positive phrasing in the body; one short tail line is fine ("No subtitles, no
  on-screen text.").

## Good vs bad

Bad (caption, no camera, vague audio):
> A man answers a phone in the rain, cinematic, dramatic, epic sound.

Good:
> Medium close-up, eye level, slow push-in from chest to face. A tired man in his fifties with a
> grey stubble beard and a soaked green trench coat lifts a rotary phone off a brick wall, under a
> buzzing green neon sign. Rain streaks through the neon light; his breath fogs. 35mm film, soft
> grain. Dialogue: The man in the green trench coat says: "Tell me she's alive." (barely a
> whisper). SFX: the receiver clicks off its hook. Ambient noise: heavy rain on a metal awning, a
> distant siren. Music: none. (no subtitles)

## Failure modes

| Symptom | Fix |
|---|---|
| Invented laugh track or music | always write Ambient noise and Music lines (Music: none) |
| Burned-in captions | `(no subtitles)`; repeat "No subtitles." once if it persists |
| Rushed or cut dialogue | shorten to <= 3 short sentences per 8 s |
| Wrong speaker talks | tag lines by visual descriptor; one speaker per beat |
| Very similar takes | change the prompt wording, not just the key |
| Vertical asked, 16:9 delivered | set `aspect` 9:16 in config; compose "vertical frame" in words |

## Self-check
- [ ] Camera sentence first; one move with start and end
- [ ] 80 to 180 words; no boosters
- [ ] Audio block present if `audio=true` (Dialogue / SFX / Ambient noise / Music)
- [ ] Dialogue fits the duration; `(no subtitles)`
- [ ] References mode => duration 8 in config

Sources: Google Cloud "Ultimate prompting guide for Veo 3.1" (camera-first, SFX/Ambient labels,
as summarized by secondary guides), predis-prompting/references/veo.md.
