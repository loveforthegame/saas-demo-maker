# LTX (LTX 2.5 Pro, LTX 2.5 Fast, LTX 2.3 Pro, LTX 2.3 Fast)

**Model facts (at the time of writing; confirm in your provider):** all four take 16:9 and 9:16,
first + last frame, and native audio (on by default on some providers).
- LTX 2.5 Pro: 720p or 1080p; 6, 8 or 10 s. Premium.
- LTX 2.5 Fast: 720p to 4K; 6 to 20 s (even numbers). Mid.
- LTX 2.3 Pro: 1080p, 1440p or 4K; 6, 8 or 10 s. Cheap.
- LTX 2.3 Fast: 1080p to 4K; 6 to 20 s (even numbers). Cheapest; priced per second.

Check the provider's model options for the exact parameter names (duration, resolution, first/
last frame, audio on/off).

## When to pick it

- **Use for:** long single takes up to 20 s cheaply, high-res (1440p / 4K) output, controlled
  A-to-B with first + last frame at low cost, macro and atmosphere, cheap motion drafts (2.3 Fast).
- **Not for:** hard cuts inside one clip, 1:1 or 4:5, anything under 6 s.

## Compile

- **Form:** one flowing paragraph, present tense, 4 to 8 sentences, chronological. No line breaks,
  no lists, no labels. Chain beats with "as", "then", "while".
- **Slot order:** shot framing -> scene -> action unfolding -> character -> camera movement ->
  audio.
- **Length:** 4 to 8 sentences. Detail scales with shot size: close-ups need more texture and
  micro-movement; wides need less.
- **Timing:** no timestamps or shot labels; it is a one-take model. Sequence with "then", "as",
  "until".
- **Camera end state:** say where the camera ends up. LTX finishes moves better when it knows the
  end framing.
- **Emotion:** physical cues ("her eyebrows lift slightly"), not labels.
- **References:** first and last frame only.
- **Audio:** inside the paragraph, last: ambient, effects, dialogue in quotes.
- **When a reference carries it:** image to video, describe the source image briefly and build on
  it, then the motion. First + last frame: describe the transition.
- **Negatives:** a short closing "avoid flicker" style clause is tolerated; keep it to one clause.

```
[Shot framing and lens]. [Scene and light]. [Subject trait line] [first action], then [second
action] as [environment reacts]. The camera [move, speed] until [describe what the frame shows
when the move ends]. [Audio: ambient, effects, dialogue in quotes].
```

### Example

Bad (labels, fragments):
> Shot 1: boxer. Shot 2: falls. Camera: zoom. Style: cinematic, 4K.

Good:
> A wide low-angle shot from the ring corner on a 24mm lens. Warm tungsten beams cut through dust
> above a worn blue canvas. The giant bearded boxer in red satin shorts tips backward from his
> heels, then sails through the air in slow motion as sweat drops spray into the light, while the
> small boy in blue gloves stays frozen with his glove out. The camera holds still until the boxer
> lies flat on his back and a puff of dust settles around him. Muffled crowd gasps fill the gym.

## Self-check

- [ ] Single paragraph, present tense, 4 to 8 sentences
- [ ] End of every camera move described
- [ ] Duration is an allowed value (6 s or more)

## Failure modes

| Problem | Fix |
|---|---|
| Move never completes | describe the end framing after the move |
| Rewritten into something else | the host may run a prompt rewriter; be concrete, not poetic |
| Unwanted cut | it is a one-take model; remove any "shot" labels |

## Field notes

- LTX 2.3 Fast works as a cheap draft model: lock the look on an image model, animate with
  motion + camera only, then promote the prompt (see the draft workflow in wan.md).
- Keep it literal: one action chain, one move, one ambient detail.

Sources: Lightricks "Prompting Guide for LTX-2" (docs.ltx.video, via search summary);
RunDiffusion LTX-2 guide; internal production field notes.
