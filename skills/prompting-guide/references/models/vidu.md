# Vidu Q3

**Model facts (at the time of writing; confirm in your provider):** 360p to 1080p (720p default
on some providers); 4 to 8 s; 16:9, 9:16, 1:1, 4:3, 3:4; native audio (on by default on some
providers). Two reference modes: **references** = up to 4 images (subject, character or style
lock), or **keyframes** = first + last frame. **Keyframes mode ignores the aspect setting: the
frame's own shape wins.** Mid cost.

Check the provider's model options for the exact parameter names (duration, aspect, audio on/off,
reference or keyframe slots).

## When to pick it

- **Use for:** reference-to-video with up to 4 subjects (characters, product, prop), short native
  audio scenes with tone-led delivery.
- **Not for:** clips over 8 s, aspect control when using keyframes.

## Compile

- **Slot order:** shot size + lens feel -> subject (by ref) -> action order -> one camera
  instruction -> light -> dialogue/sound.
- **Length:** 40 to 100 words. Concise: long prompts drift.
- **Timing:** sequence with "then"; one beat chain per clip.
- **Camera:** one camera instruction per shot. Conflicting moves lower the hit rate.
- **References:** by position in the reference list: "the barista from image 1", "the cup from
  image 2".
- **Audio:** dialogue as `[Speaker] says: "[line]"` with delivery as sensory cues ("soft smile in
  the voice", "whispered", "close mic", "warm") rather than technical specs. Effects named. Music
  "low under the dialogue". Add "No risers or whooshes" unless you want them.
- **When a reference carries it:** keyframes mode, make the frame images in the target aspect
  first, then describe only the motion between them.

```
[Shot size], [lens feel]. The [role] from image 1 [action], then [action]. Camera: [one move].
[Light]. [Speaker] says: "[line]" ([sensory delivery: whispered, close mic, warm]).
Sound: [effects]; music low under the dialogue. No risers or whooshes.
```

### Example

Bad: `cinematic epic scene with all four images doing lots of things, dynamic camera`
Good: `Medium close-up, 50mm feel. The barista from image 1 slides the cup from image 2 across the
counter, then smiles. Camera: slow push-in. Morning window light from frame left. She says:
"On the house." (warm, close mic). Sound: cup scrapes on wood; café murmur. No risers or whooshes.`

## Self-check

- [ ] 100 words or fewer, one camera instruction
- [ ] Duration 4 to 8 s; aspect handled for keyframes mode

## Failure modes

| Problem | Fix |
|---|---|
| Unwanted SFX or risers | "No risers or whooshes unless specified" |
| Wrong aspect in keyframes mode | make the frames in the target aspect |
| Drift on long prompt | 100 words or fewer |

## Field notes

No extra field notes beyond the general cheap-draft habits (see wan.md): keep it literal, one
action, one move; vary the wording if takes look identical.

Sources: Cutout.pro Vidu Q3 native audio guide; CometAPI Vidu Q3 how-to (third-party).
