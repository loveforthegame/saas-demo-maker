# Gemini Omni Flash (`gemini_omni_flash`)

**Predis options:** `resolution` 360p|720p|1080p|4k (default 720p), `aspect` 16:9|9:16. **No
duration option: it chooses its own length.** Ref mode `references`: 1 video (<= 10 s) + up to 10
images. t2v, i2v, v2v. 5 cr/s (default ~27). Makes audio by default.

**Use for:** cheapest acceptable all-rounder, plain-language edits of a clip, extensions, kinetic
text ("one word on screen at a time"), timed montages.
**Not for:** a shot that must be an exact length, premium hero shots.

## Compile

Order: **continuity statement -> subject + action -> timing -> sound -> constraint tail**.
40 to 120 words. It builds a mini-narrative with several shots unless told otherwise.

```
Single continuous shot, no scene cuts. [Subject] [action]. [Timing: "After 2 seconds, ..." or
[0-3s] ... [3-6s] ...]. Sound design: [ambient], [effects]; [music or "no music"]. No dialogue.
```

- References: native tags `<IMAGE_REF_0>`, `<VIDEO_REF_0>` numbered from 0 in reference_ids
  order, e.g. "the woman <IMAGE_REF_0> holds the bottle <IMAGE_REF_1>". End with "Use the given
  images as references, not as literal first frames."
- To control length, write the timeline ("[0-4s] ... [4-6s] ...") and say "6 seconds total".
- Edits: short, one change, then "Keep everything else the same." Strip source audio if you want
  new sound.
- Short negative lines work here: "No dialogue. No extra sound effects."
- Text on screen: quote it exactly; it renders readable text.

## Good vs bad
Bad: `In the video of the man on the sofa, add a small black cat that runs in from the right,
jumps, lands, then curls up while he pets it and smiles and the light changes...`
Good: `Add a small black cat that jumps onto his lap; he pets it. Keep everything else the same.`

## Failure modes

| Symptom | Fix |
|---|---|
| Unwanted cuts / story | "Single continuous shot, no scene cuts." first |
| Random music or voice | describe the audio or "No dialogue. No music." |
| Long edit prompt changes everything | one change per pass |

## Self-check
- [ ] Continuity line first (unless a montage is wanted)
- [ ] Tags numbered from 0 in reference order
- [ ] Audio stated

Sources: google-gemini/gemini-skills (gemini-omni-flash-api), predis-prompting/references/gemini-omni.md.
