# Model router

Picks a model family per shot. Cost words (cheap / mid / premium) are relative and were true at
the time of writing; prices, limits and model names move. Check your provider's price and model
options before every job.

## How to pick (in this order)

1. **Hard inputs first.** What must the model accept? First frame, last frame, N identity refs, a
   video ref, an audio ref, native audio, a duration under 3 s or over 10 s. Drop every model that
   cannot (see "Input map").
2. **Shot type** -> the row in the router table.
3. **Priority + budget** -> column. Hero shots = default or premium; support shots = default;
   filler and drafts = cheap.
4. **Sound plan.** If sound is added in the edit, prefer models where audio off is cheaper (Kling 3
   family on some providers) and switch audio off. If the shot needs lip-sync, only native-audio
   models or an audio-reference model qualify.
5. Write one line per shot: `S6 -> Kling 3 Pro (fast-action, hero, physics), audio off, 5 s`.

## Router table: images

| Shot type | Default | Cheap draft | Premium | Why |
|---|---|---|---|---|
| hero-still / keyframe (photoreal) | Nano Banana Pro | Nano Banana 2.1 | GPT Image 2.5 Sunburst, high quality | natural-language reasoning, up to 14 refs |
| character-sheet / consistent cast stills | Nano Banana Pro + refs | Seedream 4.5 + refs | GPT Image 2.5 Flare + refs | multi-ref identity; Seedream good at turnarounds |
| text-graphic (poster, thumbnail, UI, ad copy) | GPT Image 2.5 Flare, high quality | Ideogram 4.5 | Ideogram V3 Quality (logos, typography) | GPT Image renders quoted text verbatim |
| fix text in an existing image | Ideogram 4.5 Precise Edit | GPT Image 2 edit | | source slot + local edit |
| vector-flat / icon / brand mark | Recraft V3, digital illustration style | FLUX.2 Pro | | style setting sets the medium |
| product-still | Nano Banana Pro + product ref | FLUX.2 Pro + hex colours | FLUX.2 Max | FLUX holds hex colours tied to objects |
| draft-still (composition, moodboard) | FLUX.1 schnell | P-Image | Krea 2 Turbo | near free; no text, no refs |
| stylized / bold still | Grok Imagine Image 2 | Seedream 5 Lite | Seedream 5 Pro | |

## Router table: video

| Shot type | Default | Cheap draft | Premium | Why |
|---|---|---|---|---|
| establishing / environment | Veo 3.1 Fast | Wan 2.7 | FLUX 3 video (21:9 to 9:16, up to 20 s) | dense scene prose; ultra-wide on FLUX 3 |
| character-performance (face/body beat, no lines) | MiniMax H3 Max | Seedance 1.5 Pro | Kling O3 Pro + identity refs | H3 is fast and strong on one-beat acting; cheap retakes |
| dialogue-lipsync (native voice) | Veo 3.1 | Veo 3.1 Fast | Kling 3 Pro, audio on | Veo does dialogue + SFX + ambience in one pass |
| lip-sync to a voice file you have | Wan 2.5 i2v + audio ref | Seedance 2.0 + audio ref | DreamActor M2 (driving video) | audio slot drives mouth and rhythm |
| avatar / talking head (one portrait, speaks to camera) | Wan 2.5 i2v + voice file | Seedance 2.0 + audio ref | Veo 3.1 (native dialogue, first frame) | portrait + voice in; face large, camera calm |
| fast-action / physics / stunts | Kling 3 Pro, audio off | Kling 2.5 Turbo | Seedance 2.5 | Kling 3 most reliable with bodies, weight, contact |
| crowd / ensemble energy | Seedance 2.0 (720p) | Seedance 2.0 Fast | Seedance 2.5 | many bodies moving coherently |
| identity-locked-motion (same face across shots) | Kling O3 Pro, first frame + up to 4 refs | Seedance 2.0 Fast + refs | Kling 3 Omni (7 refs) | first frame AND identity refs in one call |
| multi-shot-sequence in one clip | Seedance 2.0 (10 to 15 s) | Seedance 2.0 Fast | Seedance 2.5 (up to 30 s + audio) | labelled shots honoured; Kling 3 Pro also cuts on labels |
| product-motion / controlled arc (A to B) | Kling 3 Standard, first + last, audio off | LTX 2.3 Pro, first + last | Veo 3.1 keyframes | last-frame slot locks the end state |
| macro-texture / liquids / light | Veo 3.1 (4 s) | LTX 2.3 Fast | LTX 2.5 Pro | |
| stylized-anime | Grok Imagine Video 1.5 | Seedance 1.5 Pro | Seedance 2.0 + style ref | plain-named medium works on Grok |
| short-insert (edit keeps under 2 s) | Grok Imagine Video 1.5 (1 s steps) | Seedance 1 Pro (2 s minimum) | Kling O3 Pro (3 s) | do not pay for 5 s you will cut |
| long-take (over 10 s, one shot) | LTX 2.3 Fast (up to 20 s) | Wan 2.7 (up to 15 s) | Seedance 2.5 (up to 30 s) | |
| motion draft before a hero run | Wan 2.2 i2v Fast | Seedance 1.5 Pro | Kling 2.5 Turbo | test motion and blocking, then promote the prompt |
| restyle an existing clip | Runway Aleph 2 | Wan 2.7 video edit | Kling 3 Omni + refs | one change per pass + keep line |
| extend a clip | Grok Video Extension | Gemini Omni Flash | | continue from the observed last frame |
| motion-transfer | DreamActor M2 | Seedance 2.0 video ref | | image gives identity, video gives motion |
| all-rounder, cheapest acceptable | Gemini Omni Flash (picks its own length) | | | |

## Family -> file

| Family | File |
|---|---|
| Veo 3.1, Veo 3.1 Fast | models/veo.md |
| Kling 2.x, Kling 3, Kling O3 Pro, Kling 3 Omni | models/kling.md |
| Seedance 1.x, Seedance 2.x | models/seedance.md |
| MiniMax H3, Hailuo | models/minimax-hailuo.md |
| LTX 2.3 / 2.5 | models/ltx.md |
| Wan 2.2 / 2.5 / 2.7 | models/wan.md |
| Gemini Omni Flash | models/gemini-omni.md |
| Vidu Q3 | models/vidu.md |
| Grok Imagine Video, Grok Video Extension | models/grok-video.md |
| FLUX 3 video | models/flux-video.md |
| Runway Aleph, Wan video edit, DreamActor, extensions | models/video-edit-restyle.md |
| Nano Banana | models/nano-banana.md |
| GPT Image | models/gpt-image.md |
| Seedream | models/seedream.md |
| FLUX images | models/flux-image.md |
| Ideogram | models/ideogram.md |
| Recraft | models/recraft.md |
| Qwen, MAI, Grok Image, Krea, P-Image + rules for every image model | models/image-others.md |

## Input map (at the time of writing; confirm in your provider)

| Need | Models that accept it |
|---|---|
| first + last frame | Veo 3.1 (+ Fast), Kling 3 Pro / Standard, Kling 2.1, Seedance 2.0 (+ Fast), Seedance 2.5, Seedance 1.5 Pro, Seedance 1 Pro, Hailuo 3, MiniMax H3 Max, Wan 2.7, LTX (all four), FLUX 3 video, Vidu Q3, Gemini Omni Flash |
| first frame only | Kling 2.6, Kling 2.5 Turbo, Seedance 1 Lite, Wan 2.2 i2v Fast, Wan 2.5 i2v, Grok Imagine Video 1.5, Kling O3 Pro |
| first frame + identity refs in one call | Kling O3 Pro (1 + 4) |
| identity / style refs (no first frame) | Veo 3.1 (3, locks 8 s), Seedance 2.0 (9), Seedance 2.5 (30), Kling 3 Omni (7 + 1 video), Hailuo 3 (9), Gemini Omni Flash (10), Vidu Q3 (4), Grok Imagine Video 1.5 (7, locks 720p) |
| video ref | Seedance 2.x, Kling 3 Omni, Hailuo 3, Gemini Omni Flash, Runway Aleph 2, Wan 2.7 video edit, DreamActor M2, Grok Video Extension |
| audio ref | Seedance 2.x, Hailuo 3, Wan 2.5 i2v |
| native audio | Veo 3.1, Kling 3, Kling O3 Pro, Kling 2.6, Kling 3 Omni, Seedance 2.x, Seedance 1.5 Pro, LTX, FLUX 3 video, Vidu Q3, Gemini Omni Flash |
| durations | Veo 4/6/8 s; Kling 3 5-10; Kling O3 3-15; Kling 3 Omni 3-15; Seedance 2.0 4-15; Seedance 2.5 4-30; Seedance 1 Pro/Lite 2-12; MiniMax/Hailuo 5-15; Wan 2.7 2-15; LTX Fast 6-20; LTX Pro 6-10; Grok 1-15; Vidu 4-8; FLUX 3 video 5-20 |
| aspect beyond 16:9 / 9:16 / 1:1 | Seedance, MiniMax/Hailuo, Wan 2.7, Vidu, Grok, FLUX 3 video (21:9) |
| negative prompt or seed field | none found on any model in one provider's listing; may exist elsewhere |

## Cost levers worth knowing

- Kling 3 Pro: audio off is about a third cheaper than audio on (some providers). Kling O3 Pro
  also cheaper with audio off. Seedance 2.0 and Veo: audio does not change the price.
- Seedance 2.0 at 1080p costs about 2.5x 720p. Draft at 720p.
- Duration is linear on most models: a 3 s Kling O3 shot costs about 60 % of a 5 s one.
- Hero shots: budget 2 retakes. Performance and dialogue shots: 2 to 3 takes, keep the clean one.
