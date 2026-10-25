# Vidu Q3 (`vidu_q3`)

**Predis options:** `resolution` 360p|540p|720p|1080p (default 720p), `duration` int 4-8,
`aspect` 16:9|9:16|1:1|4:3|3:4, `audio` (default true). Ref modes: `references` = up to 4 images
(subject/character/style lock), or `keyframes` = first + last frame (**keyframes mode ignores
aspect**: the frame's own shape wins). 13 cr/s.

**Use for:** reference-to-video with up to 4 subjects (characters, product, prop), short native
audio scenes with tone-led delivery.
**Not for:** > 8 s, aspect control when using keyframes.

## Compile

Order: **shot size + lens feel -> subject (by ref) -> action order -> one camera instruction ->
light -> dialogue/sound**. 40 to 100 words. Concise: long prompts drift.

```
[Shot size], [lens feel]. The [role] from image 1 [action], then [action]. Camera: [one move].
[Light]. [Speaker] says: "[line]" ([sensory delivery: whispered, close mic, warm]).
Sound: [effects]; music low under the dialogue. No risers or whooshes.
```

- One camera instruction per shot (conflicting moves lower the hit rate).
- Delivery as sensory cues ("soft smile in the voice", "close mic") rather than technical specs.
- Keyframes mode: make the frame images in the target aspect first.

## Good vs bad
Bad: `cinematic epic scene with all four images doing lots of things, dynamic camera`
Good: `Medium close-up, 50mm feel. The barista from image 1 slides the cup from image 2 across the
counter, then smiles. Camera: slow push-in. Morning window light from frame left. She says:
"On the house." (warm, close mic). Sound: cup scrapes on wood; café murmur. No risers or whooshes.`

## Failure modes

| Symptom | Fix |
|---|---|
| Unwanted SFX/risers | "No risers or whooshes unless specified" |
| Wrong aspect in keyframes mode | frames in target aspect |
| Drift on long prompt | <= 100 words |

## Self-check
- [ ] <= 100 words, one camera instruction
- [ ] Duration 4-8; aspect handled for keyframes mode

Sources: Cutout.pro Vidu Q3 native audio guide; CometAPI Vidu Q3 how-to (third-party).
