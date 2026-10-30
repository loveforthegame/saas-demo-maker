# Gemini Omni Flash

**Model facts (at the time of writing; confirm in your provider):** 360p to 4K (720p default on
some providers); 16:9 and 9:16. **Usually no duration option: it picks its own length.** Text to
video, first frame to video, first + last frame transitions, image and video references (1 video
up to about 10 s + up to 10 images), edits of an existing clip, and extensions. Makes audio by
default. Cheap; priced per second.

Which of these modes your provider exposes, and the parameter names for resolution, aspect and
references: check the provider's model options.

## When to pick it

- **Use for:** cheapest acceptable all-rounder, plain-language edits of a clip, extensions,
  kinetic text ("one word on screen at a time"), timed montages, readable on-screen text.
- **Not for:** a shot that must be an exact length, premium hero shots.

## Compile

- **Slot order:** continuity statement -> subject + action -> timing -> sound -> constraint tail.
- **Length:** 40 to 120 words.
- **Continuity:** it builds a mini-narrative with several shots unless told otherwise. For one
  scene start with "Single continuous shot, no scene cuts."
- **Timing:** natural language works ("After 3 seconds, a woman enters." "At 5s the chorus
  starts." "Every 2s cut to a new location." "Rapid fire: every half second (12 frames at 24fps)
  a new scene."). Timecodes work too. To control length, write the timeline and the total:
  "[0-4s] ... [4-6s] ... 6 seconds total".
- **References (model-native tags; syntax may differ by provider):**
  - `<FIRST_FRAME>` start image; `<LAST_FRAME>` end image (only with a first frame). Same image
    for both = a loop.
  - `<IMAGE_REF_0>`, `<IMAGE_REF_1>` ... image references, numbered from 0 in the reference list
    order.
  - `<VIDEO_REF_0>` ... video references for character, object or motion style (about 3 s each
    is ideal, up to 3).
  - Example: "the woman <IMAGE_REF_0> holds the bottle <IMAGE_REF_1>"; "in the style of
    <IMAGE_REF_0>, the woman <IMAGE_REF_1> is walking" (style from the first, subject from the
    second).
  - End with a plain guide line: "Use the given images as references, not as literal first
    frames." or "Use the given videos as references, not as a source to edit."
  - If your provider assigns roles itself, keep the reference list in the same order as the tag
    numbers.
- **Audio:** it makes a track by default. Describe the audio you want, especially music ("calm
  background music", "high-energy techno beat", "tinny radio playing in the background"), or
  write "No dialogue. No music."
- **Negatives:** short negative lines work here: "No dialogue. No embellishments. No extra sound
  effects."
- **On-screen text:** quote it exactly; it renders readable text.
- **When a reference carries it:** for edits, the clip carries everything; write one change,
  then "Keep everything else the same."

```
Single continuous shot, no scene cuts. [Subject] [action]. [Timing: "After 2 seconds, ..." or
[0-3s] ... [3-6s] ...]. Sound design: [ambient], [effects]; [music or "no music"]. No dialogue.
```

### Examples

Single scene:
> Continuous, unbroken handheld shot of a fluffy tabby cat on a sunny windowsill, looking out at a
> leafy garden. Its tail twitches slowly and its ears turn toward sounds. Sunbeams light dust in
> the air. Sound design: gentle breeze, distant birds. No dialogue.

Edit, bad: `In the video of the man on the sofa, add a small black cat that runs in from the
right, jumps, lands, then curls up while he pets it and smiles and the light changes...`
Edit, good: `Add a small black cat that jumps onto his lap; he pets it. Keep everything else the
same.`

Multi-subject shape:
```
[0-3s] Studio fashion sequence. The woman <IMAGE_REF_0> holds <IMAGE_REF_1>.
[3-6s] The man <IMAGE_REF_2> holds <IMAGE_REF_3>.
[6-10s] Another woman <IMAGE_REF_4> walks holding <IMAGE_REF_5>.
```

## Self-check

- [ ] Continuity line first (unless a montage is wanted)
- [ ] Tags numbered from 0 in reference list order
- [ ] Audio stated
- [ ] Timeline + total written if length matters

## Failure modes

| Problem | Fix |
|---|---|
| Unwanted cuts or story | "Single continuous shot, no scene cuts." first |
| Random music or voice | describe the audio, or "No dialogue. No music." |
| Long edit prompt changes everything | one change per pass, then "Keep everything else the same." |
| Wrong length | write the timeline and "N seconds total" |

## Field notes

### Meta instructions it follows

- "Consider micro-detail, expression and timing to create a rich but natural scene."
- "Be extremely specific about the people, costumes, items and background."
- "Show a different rare [thing] every 1s, upbeat music, label each with text."

### Text in video

Define any text that would naturally appear, even in the background: a street sign that says:
"Open Late"; a car plate: "OMNI1". Kinetic words: "One word on screen at a time: did, you, know.
Each word for 1s in a different animated style. No dialogue."

### Editing an existing clip

- Simple beats descriptive. "Make this video anime." "Put a fashionable hat on this person."
  "Change the lighting to be more dramatic." "Change the text on the sign to say "Grand
  Opening"."
- Removal: avoid a paragraph about removing a phone. Use: "Make the phone invisible. Keep
  everything else the same."
- Audio: if the source clip has sound, the model keeps and adapts it. For all-new sound, strip the
  audio before upload: `ffmpeg -i in.mp4 -an -c:v copy silent.mp4`.
- Source clips work best around 10 s, 720p, 24fps. Trim and scale first:
  `ffmpeg -i in.mp4 -t 10 -vf "scale=-2:720,fps=24" prep.mp4`.

### Extending

- "Extend this video" or "The scene continues" plus what happens next. It uses the last seconds
  of the input as context and may retouch the final input frames for a seamless join.
- Timestamps in an extension prompt count from the start of the new part.
- Say whether the scene continues or cuts ("show the same characters in the next scene") and what
  the audio does ("the music continues into the chorus").
- References can introduce a new character or object into the extension.
- Uploaded clips where someone talks cannot be extended with new dialogue; silent characters are
  fine.

Sources: google-gemini/gemini-skills (gemini-omni-flash-api); internal production field notes.
