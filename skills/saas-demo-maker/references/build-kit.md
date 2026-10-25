# Build kit (HyperFrames)

One monolithic `film/index.html`. Load the `hyperframes` + `hyperframes-core` skills for the composition contract; this file holds only what is specific to these ads. CLI: `npx --yes hyperframes@<pinned version>` (`lint`, `snapshot --at …`, `render -f 60 -o renders/<name>.mp4`).

## Project layout

```
<project>/
  BRIEF.md  STORYBOARD.md  NOTES.md          # intake, signed table, per-round feedback log
  predis-output/director/<slug>/SHOTS.md     # cast bible, compiled prompts, run log (predis-director)
  assets/gen/                                # every generated still + contact sheets
  film/index.html  film/assets/{img,video,audio,brand,fonts}  film/renders/  film/versions/
```
Copy `assets/audio/sfx/` and `assets/fonts/inter-var.woff2` from this skill into `film/assets/`. Music: a Mixkit track the user hasn't heard in an earlier ad.

## Layers (DOM order = paint order)

1. `.cam > video` per live cut (`data-start`, `data-duration`, `data-media-start`, `data-playback-rate`). A `<video data-start>` must not sit inside a timed `<section>`.
2. `<section class="clip scene">` overlays for live beats (lower-third, captions, bubbles).
3. `<section id="ui">` = brand canvas + `.world` (all product cards) + letterbox bars.
4. Shared-motif layer (e.g. droplets) as its own clip so it survives the live→UI cut.
5. End lockup section, grain, audio.
Anything that flies onto another card needs a higher `z-index` or a later DOM position.

## Helpers (paste once)

```js
const tl = gsap.timeline({ paused: true });
const crashIn = (sel, t, from) => tl.fromTo(sel, { scale: from || 1.35, filter: "blur(6px)" }, { scale: 1, filter: "blur(0px)", duration: 0.2, ease: "expo.out" }, t);
const snapOut = (sel, t, to) => tl.to(sel, { scale: to || 1.35, filter: "blur(8px)", duration: 0.13, ease: "power4.in" }, t);
// world-space virtual camera: animate a plain object, write the transform onUpdate (tweening the element itself fights the transform string)
const world = document.getElementById("world"), cam = { s: 1, x: 0, y: 0 };
const applyCam = () => { world.style.transform = `translate(${cam.x}px,${cam.y}px) scale(${cam.s})`; };
const V = (s, cx, cy) => ({ s, x: 960 - s * cx, y: 540 - s * cy });          // frame point (cx,cy) of the world at scale s
const move = (a, b, t, d, ease) => tl.fromTo(cam, { ...a }, { ...b, duration: d, ease, onUpdate: applyCam, immediateRender: false }, t);
// whip (Creatify 7.3): power4.inOut + horizontal SVG blur peaking mid-move; world has filter:url(#hblur)
const hb = document.getElementById("hblurE");  // <filter id="hblur"><feGaussianBlur id="hblurE" stdDeviation="0 0"/></filter>
const whip = (a, b, t, d) => { move(a, b, t, d, "power4.inOut");
  tl.fromTo(hb, { attr: { stdDeviation: "0 0" } }, { attr: { stdDeviation: "38 0" }, duration: d / 2, ease: "power2.in", immediateRender: false }, t);
  tl.to(hb, { attr: { stdDeviation: "0 0" }, duration: d / 2, ease: "power2.out" }, t + d / 2); };
const holo = (sel, t) => tl.fromTo(sel + " .holo", { opacity: 0.95, filter: "hue-rotate(0deg)" }, { opacity: 0, filter: "hue-rotate(180deg)", duration: 0.6, ease: "power2.out" }, t); // Creatify 7.9
window.__timelines = { main: tl };
```
`.holo { position:absolute; inset:0; background: conic-gradient(from 30deg,#ff9ad5,#7cf5ff,#c4ff7a,#b38cff,#ff9ad5); mix-blend-mode: difference; opacity:0 }`

## Patterns that passed review

- **Live → UI through an object (Creatify 7.7):** zoom the live clip into the phone/screen in the hero's hand (`scale 3, transformOrigin = object point, blur 10px`, 0.2 s `power2.in`), then open the UI with `clipPath: circle(0 → 2300px at the same point)`, 0.4 s `expo.inOut`, and start the camera from `V(0.75, objX, objY)`.
- **J-cut voice:** extract the take's audio (`ffmpeg -i take.mp4 -vn -t <s> voice.wav`), play it from t=0 under the opening shot, start the picture later with `data-media-start` = its film start, mute the video element. Lips stay in sync.
- **Silence impact:** split a clip into two `<video>` elements and set the second one's `data-volume="0"`.
- **Prompt typing with hot characters (M8):** split into spans; each char appears in the accent colour, settles in ~0.15 s; ~80 chars/s for short prompts.
- **Plan/status line (jungle 7.6):** `background-clip:text` with a gradient sweep from ink to grey over 0.3 s.
- **Outputs burst (T1 + Creatify 7.9):** a shared-motif element flies to each slot, scales out, the card pops `back.out(2.2)` 0.22 s, holo develops 0.6 s. Hold ≥0.4 s before moving them.
- **Click (T6, add T5 only if the button stays visible):** cursor glide 0.25 s on curved path (x and y on different eases), dwell ~0.3–0.4 s, press = brightness 1.35 + scale 0.95, then colour change + ripple. Under a letterbox, push the camera into the button first ("shoot it as a crop").
- **Fan-out to destinations (T1/T15):** per output, small motif elements fall to each destination icon (`power2.in` on y, `power1.inOut` on x), splash ring + check badge, status chips pop in sequence 0.06–0.1 s apart.
- **Payoff bubble (pool lady 7.9):** white pill with a tail, `transformOrigin` at the tail, `back.out(2.5)` 0.22 s, from the real phone/screen in the shot.
- **Lockup (T19 + T11):** logo `scale 4.2 → 1, blur 10 → 0`, 0.2 s `expo.out`; tagline words arrive accent → ink; CTA line; whole lockup drifts `scale 1.025` over the hold.

## Checks (run every render)

```bash
# timestamped frame grid to pick media-start points
ffmpeg -i clip.mp4 -vf "fps=6,scale=400:-1,drawtext=text='%{pts\:hms}':x=8:y=8:fontsize=26:fontcolor=yellow:box=1:boxcolor=black" -frames:v 30 /tmp/f-%02d.png && ffmpeg -i /tmp/f-%02d.png -vf tile=6x5 grid.jpg
# spoken lines with word times
whisper clip.mp4 --model base --language en --word_timestamps True --output_format json --output_dir <dir>
# duration + loudness of the render (target about -16 to -19 LUFS integrated)
ffprobe -v error -show_entries format=duration -of csv=p=0 film.mp4
ffmpeg -i film.mp4 -af ebur128 -f null - 2>&1 | grep " I:"
```
Snapshot before every render: `snapshot --at <every beat start>,<every hand-off> --no-end` and read the contact sheet.

## Gotchas

- Seedance clips arrive at ~1284×716; the 1080p render is an upscale. Say so.
- A whip/zoom tween and a drift tween on the same property overlapping → lint warning and a jump; end one before the next starts.
- `z-index:-1` children need `isolation: isolate` on the parent.
- Keep a live video running under a circle-wipe hand-off, or the wipe reveals black.
- On Windows Git Bash, don't pipe long Python through heredocs with quotes; write the script to a file and run it.
