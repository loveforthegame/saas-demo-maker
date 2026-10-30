# Veo 3.1 (Veo 3.1, Veo 3.1 Fast)

**Model facts (at the time of writing; confirm in your provider):** clips of 4, 6 or 8 s;
16:9 and 9:16 only; 720p, 1080p and 4K; native audio on by default (dialogue, effects, ambience
and music in one pass). Two reference modes: **references** (up to 3 images as identity or style
"ingredients", which locks duration to 8 s) and **keyframes** (first frame + last frame).
Cost: Veo 3.1 is premium; Veo 3.1 Fast is mid-to-cheap. Turning audio off does not lower the
price on most providers, so a free scratch track is worth keeping. Check your provider's model
options for the exact parameter names (duration, aspect ratio, audio on/off, first/last frame
and reference slots).

## When to pick it

- **Use for:** dialogue with lip-sync, shots where sound sells it, macro, liquids and light.
  Draft on Veo 3.1 Fast, finish on Veo 3.1 with the identical prompt.
- **Not for:** 1:1 or 4:5, shots over 8 s, cheap filler, current events or real people (no live
  knowledge).

## Compile

- **Slot order:** camera -> subject -> action -> setting -> light -> style -> audio block.
  Cover all seven layers: subject, context, action, style, camera, composition, ambiance.
- **Length:** 80 to 180 words. Veo rewards dense, concrete prose. Overdescribe the concrete
  parts; it does not reward adjectives.
- **Timing:** for 2 to 3 beats in one clip use timestamp brackets `[00:00-00:02] ...
  [00:02-00:05] ...`. More than 3 beats in 8 s: split the shot.
- **References:** references mode, say each ingredient's job ("the man from image 1, the jacket
  from image 2"). Remember duration becomes 8 s.
- **Audio:** a four-line block, Dialogue / SFX / Ambient noise / Music (see Field notes).
  Audio off: switch it off in the provider and drop the audio block.
- **When a reference carries it:** keyframes mode, describe only the motion and sound between
  the frames. Image-led shots: generate the look first on an image model, pass it as the first
  frame and describe only motion, camera and sound; style, grade and composition carry through.
- **Negatives:** positive phrasing in the body; one short tail line is fine ("No subtitles, no
  on-screen text.").

Template:

```
[Shot size], [angle], [one camera move with start and end]. [Subject trait line] [action with
endpoint], [setting]. [Light sources]. [Look line].
Dialogue: [Speaker tag] says: "[line]" ([delivery]).
SFX: [sound] as [action]. Ambient noise: [place sound]. Music: [genre/mood or "none"].
(no subtitles)
```

### Example

Bad (caption, no camera, vague audio):
> A man answers a phone in the rain, cinematic, dramatic, epic sound.

Good:
> Medium close-up, eye level, slow push-in from chest to face. A tired man in his fifties with a
> grey stubble beard and a soaked green trench coat lifts a rotary phone off a brick wall, under a
> buzzing green neon sign. Rain streaks through the neon light; his breath fogs. 35mm film, soft
> grain. Dialogue: The man in the green trench coat says: "Tell me she's alive." (barely a
> whisper). SFX: the receiver clicks off its hook. Ambient noise: heavy rain on a metal awning, a
> distant siren. Music: none. (no subtitles)

## Self-check

- [ ] Camera sentence first; one move with start and end
- [ ] 80 to 180 words; no boosters
- [ ] Audio block present if audio is on (Dialogue / SFX / Ambient noise / Music)
- [ ] Dialogue fits the duration; `(no subtitles)`
- [ ] References mode => duration set to 8 s
- [ ] Aspect set in the provider, not only in words

## Failure modes

| Problem | Fix |
|---|---|
| Invented laugh track or music | always write Ambient noise and Music lines (Music: none) |
| Burned-in captions | `(no subtitles)`; repeat "No subtitles." once if it persists |
| Rushed or cut dialogue | shorten to 3 or fewer short sentences per 8 s |
| Filler or gibberish speech | line too short for the clip; fill to about 2 sentences per 8 s |
| Wrong speaker talks | tag lines by visual descriptor; one speaker per beat |
| Very similar takes | change the prompt wording, not just the seed |
| Vertical asked, 16:9 delivered | set 9:16 in the provider; also write "vertical frame" |

## Field notes

### Audio: prompt all four layers

1. Dialogue: exact words after a colon, or described intent ("he introduces himself").
2. Ambience: the room or place ("busy festival field, distant bands, crowd murmur").
3. Effects: tied to actions ("the door slams", "glass shatters").
4. Music: genre, mood, instruments, or "no music".

Skip ambience and the model invents it (a common failure is a laughing studio audience).
Silence has to be written: "room tone only, no music, no dialogue".

### Dialogue rules

- Length fits the clip: about 2 to 3 short sentences per 8 s.
- Speaker by visual tag, never a pronoun: `The woman in pink says: ...` / `The man with
  glasses replies: ...`.
- Colon form. One source writes the line with quotes after the colon (as in the template);
  another uses the colon alone (`She says: Hello there.`). If the words render as on-screen text,
  use colon + quotes.
- Spell hard names phonetically ("Shreedar", "foh-fur").
- For clean lip-sync keep the speaker large in frame and the camera calm during the line.

### Multi-shot in one clip

Timecoded shots work as a structure:

```
[0-3s] Macro shot of a perfume bottle among pink peonies, petals drifting in warm light, soft ambient music.
[3-7s] Camera glides closer, a hand enters from the right and touches the glass, silk rustles.
[7-12s] Hard cut to slow-motion spray, golden mist catching rim light, the hiss of the atomizer.
```

Name transitions (hard cut, whip pan, seamless morph); otherwise the model improvises them.
Note the clip length cap (8 s at the time of writing) when planning timecodes.

### Scene, not caption (short form)

> A desperate man in a weathered green trench coat picks up a rotary phone mounted on a gritty
> brick wall, bathed in the glow of a green neon sign. Medium close-up, slow push-in. Rain drips
> from the awning. He says: Tell me she's alive. Sound: steady rain on metal, a distant siren,
> low tense synth pad. (no subtitles)

Sources: Google Cloud "Ultimate prompting guide for Veo 3.1" (camera-first, SFX/Ambient labels,
as summarized by secondary guides); internal production field notes.
