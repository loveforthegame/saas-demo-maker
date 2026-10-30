# Reverse mode variants: Replica, Remix, UGC + script

Three ways to use a reference video. Each one runs the base method in
[video-to-prompt.md](video-to-prompt.md) and changes only the parts listed here. Step numbers below
are that file's steps. Read the base first; nothing here repeats it.

| Variant | What stays from the reference | What is new | Main output |
|---|---|---|---|
| [Replica](#replica) | everything you can measure | nothing (or the user's own product, already in the clip) | style lock, master prompt, per-shot prompts |
| [Remix](#remix) | structure, beat grid, signature devices, energy | the product or brand | start-frame image prompts + a motion-only time-sequence prompt |
| [UGC + script](#ugc--script) | framing, camera, gestures, pacing, scene pattern | the spoken words (and often the product) | one paste-ready avatar prompt: global block + scene blocks |

Shared rule for all three: a text prompt never gives identical pixels. Aim for the closest match,
say what raises it, and never promise "exact".

---

## Replica

Recreate the reference as closely as possible. Best for product and ad videos where the user owns
the product, or wants a study of how a shot was made.

### When to use it

Trigger phrases: "copy this video", "recreate this exactly", "replicate", "clone this ad", "ditto
copy", "same video", "is video jaisa banao", "video ka prompt do", "what camera and lighting is
this", "shot-by-shot breakdown of this ad".

### Extra input to ask for

- Which segment, if the video is over about 60 s (generators work in short clips).
- Whether the product in the clip is the user's own. If yes, its label and on-screen text are
  transcribed exactly. If no, the base rule in Step 1 holds: replace people, brands and logos.
- The music track or voiceover script, if sound matters. Most generators cannot reproduce a
  specific track; use the original audio in the edit.
- The generator, only if the user cares. Do not block on it: deliver provider-neutral prompts and
  ask at the end.

### What changes vs the base method

**Step 3 (frames): add measurement.** Replica fails when you only look. Measure what eyes guess
badly:

- **Camera amount.** Read the subject's height as a percent of frame height on the shot's first
  and last frame. 45% to 56% is "the subject grows about 25% over 5 s". For lateral moves, track
  one background point: "shifts about 20% of frame width left to right".
- **Easing.** Compare the change across the 1 fps frames: even steps = constant speed; small
  steps at the ends = ease-in-out; big then small = decelerating to a settle.
- **Feel.** Small random offsets frame to frame = handheld; none = tripod or gimbal; perfectly even
  = motion control.
- **Who moves.** If the background moves too, the camera moves. If only the product turns and the
  background holds, it is a turntable. Say which in every movement line.
- **Pan vs truck, zoom vs dolly.** You cannot tell from the subject alone. Look for parallax between
  foreground and background: parallax present = a physical camera move (truck, dolly); none = a pan
  or a zoom.
- **Fine detail.** For a label, a reflection or a highlight shape, crop a zoomed frame:

  ```bash
  ffmpeg -hide_banner -loglevel error -ss <t> -i "$V" -frames:v 1 -vf "crop=iw*0.3:ih*0.3:iw*0.35:ih*0.3,scale=1280:-2" frames/zoom-<t>.jpg
  ```

  The four crop values are width, height, x, y as fractions of the frame. Change them to aim.
- **Speed ramps.** Use a Step 3 strip across the ramp. Write the slow part with times and a rough
  speed: "0.8 to 1.6 s at about 25% speed, then ramps back to 100%".
- **Loop.** Compare `first.jpg` and `last.jpg`. If they match, write "seamless loop".

**Step 5b (per shot): add these fields.** The base list covers shot, lens, move, light and grade.
Replica needs the values behind them:

| Field | Write it as |
|---|---|
| Key light | position as a clock face from camera ("10 o'clock") or degrees, height, source type and size, soft or hard |
| Fill | key-to-fill ratio: 2:1 flat, 4:1 moody, 8:1 dramatic |
| Rim, background light | which edges glow and their colour; gradient or pool behind the subject |
| Colour temperature | Kelvin: about 3200 K tungsten, 5600 K daylight; mixed sources named separately |
| Highlights on the product | the shape (long strip, window, sparkle) and whether it slides as the camera or product moves. A sliding strip highlight is a defining look in product ads. |
| Surface | glossy acrylic with a mirror reflection, marble, wood; reflection strength and blur |
| Palette | hex values read from the frames with a colour picker, each tied to an object (background, product, accent). Never invent a hex. |
| Grade | crushed or lifted blacks, highlight roll-off, tint or split-tone, grain amount |
| Product motion | rotation direction seen from above, seconds per turn, the time each beat peaks ("splash peaks at 1.8 s") |
| Text and graphics | exact words, font feel, weight, colour, position, animation in and out with timing. Still EDIT, per Step 5a. |

Screen recordings, UI demos, motion graphics and 3D: swap the lens and light rows for UI elements,
cursor path, easing curves, layer order and render style. Keep the timing exact.

**Step 6 (briefs): add a style lock and two master prompts.**

1. Expand the look line into a **style lock**: everything that must match in every shot, pasted
   word for word at the start of each shot prompt.

   ```text
   STYLE LOCK: [product: material, finish, colours, text]. [set and surface]. [key / fill / rim: direction, softness, Kelvin]. [palette: background #..., product #..., accent #...]. [grade: contrast, saturation, tint, grain]. [lens and depth of field]. [motion feel: gimbal / handheld / locked]. [one style line].
   ```

2. **Sentence order inside a shot prompt:** shot size and angle with the subject; set and surface;
   action with timing; camera move (direction, amount, speed, easing, feel); lens and depth of field;
   lighting; palette and grade; atmosphere; one style line; text overlays only if the model renders
   text (otherwise list them for the edit); audio note if the model makes sound.
3. **Pick the multi-shot strategy:**

   | Reference | Strategy |
   |---|---|
   | 1 to 3 shots, model follows labelled shots | one timeline master prompt with timecoded shots |
   | 3 or more shots, or cuts under 2 s | per-shot prompts, each opening with the style lock, stitched with the cut list (most reliable) |
   | highest fidelity wanted | image-to-video per shot with the extracted first frame (or a clean product photo) as the start frame; the prompt then carries motion, camera and light changes only |
   | average shot under 1 s | never ask one prompt to cut; per-shot prompts plus a cut list |

4. Also write the master prompt in two lengths: **full** (about 150 to 300 words, everything
   measured) and **compact** (about 60 to 90 words: subject, camera move with amount, light,
   palette, style) for character-limited tools.
5. **Negative field**, only for models that have one (`../model-router.md` input map). Start from
   this list and remove anything the reference actually shows (drop "camera shake" for a handheld
   reference, "grain" for a grainy one):

   ```text
   distorted product shape, warped or melting geometry, extra parts, duplicated objects, misspelled or garbled text, changing logo, flickering, inconsistent lighting between frames, morphing textures, sudden color shifts, unwanted camera shake, jump cuts inside the shot, watermarks, subtitles, low resolution, oversharpened halos, plastic-looking skin, extra fingers, deformed hands
   ```

   Models without the field get the essentials as positive statements ("clean product surface",
   "steady camera").

**Step 7 (deliver): add two sections.** An overview table (duration, fps, aspect, shot count and
average length, style, pacing, palette, audio) at the top. A **confidence and gaps** list at the
end: high (numbers and frames agree), medium or low (inferred lens, pan vs truck unclear), not
determinable (audio content, unreadable text) and what the user can send to close each gap. Close
with the two biggest levers: image-to-video from the extracted first frame, shot by shot; and
aspect ratio and duration set in the generator's settings, not only in the prompt text.

**Quality gate: add measured gap fixes.** After the side-by-side pairs, measure brightness and
saturation per second on both files:

```bash
ffmpeg -hide_banner -loglevel error -i reference.mp4 -vf "fps=1,signalstats,metadata=print:file=ref-stats.txt" -f null -
ffmpeg -hide_banner -loglevel error -i output.mp4 -vf "fps=1,signalstats,metadata=print:file=out-stats.txt" -f null -
```

Compare `YAVG` (brightness) and `SATAVG` (saturation) line by line, then turn each gap into one
prompt change:

| Gap | Prompt fix |
|---|---|
| duration off by more than 10% | set the duration in the generator; or generate per shot and trim |
| wrong aspect | set the aspect in the generator settings; prompt text does not control it |
| fewer or more shots than the reference | switch to per-shot prompts and stitch |
| push-in too strong or too weak | state the target: "frame grows about 25% over 5 s" |
| lateral move off | restate direction and distance from the viewer's side |
| camera feel differs | add or remove "handheld" or "gimbal-smooth" |
| output brighter | lower exposure, deeper shadows, low-key |
| output darker | add fill, raise exposure, high-key |
| contrast too high | large diffused source, lifted blacks |
| contrast too low | harder key, deeper blacks, glossy speculars |
| warmer or cooler than the reference | state the Kelvin and tint |
| saturation off | "muted, desaturated grade" or "rich, saturated colors" |
| a dominant colour missing | name its hex in the prompt, tied to its object |

If nothing measurable differs, compare product fidelity by eye.

### Output format, filled

Fictional 2-shot product film, 8.0 s, 30 fps, 16:9. Palette #0b0b0c, #c9a24a, #d9c7a3. The user
owns the product, so the engraving is transcribed.

```text
STYLE LOCK: rectangular frosted-glass perfume bottle with amber liquid (#d9c7a3) and a brushed-gold cap (#c9a24a) engraved "MAISON", on glossy black acrylic with a soft mirror reflection, pure black seamless background (#0b0b0c). Large strip light from camera right at 45 degrees giving a long vertical highlight on the glass edge, faint warm rim light behind the cap, low fill, deep shadows. Low-key, high contrast, slightly warm highlights, no grain. 85mm lens feel, shallow depth of field. Smooth gimbal motion. Slow, premium, minimalist.
```

```text
Shot 1 (5 s): STYLE LOCK: <pasted>. Medium close-up, slightly low angle, the bottle centred at about 45% of frame height. 0-5 s: the camera makes a slow push-in, the bottle grows about 25% over 5 seconds with ease-in-out; the strip-light highlight slides slowly from right to left along the glass edge as the camera moves. Fades in from black over the first 0.5 s. Start frame: frames/first.jpg. Duration 5 seconds.
```

```text
Shot 2 (3 s): STYLE LOCK: <pasted>. Hard cut. Extreme close-up of the engraved cap. 0-3 s: the camera slides left to right about 20% of frame width at constant speed; the engraving "MAISON" reads clearly; background stays pure black. Duration 3 seconds.
```

Confidence: high for the camera move, cut time and palette (numbers and frames agree); medium for
the lens (read from background compression); not determinable: the music track (user to supply).

### Pitfalls → fixes

| Pitfall | Fix |
|---|---|
| "Epic cinematic push" gives a random move | measured wording: amount, seconds, easing, feel |
| A turntable shot is written as an orbit | check whether the background moves; say who moves |
| Left and right swapped | write from the viewer's side; re-check against the frames before delivering |
| Contradictions ("static camera" + "pushing in"; "soft light" + "hard shadows") | one value per attribute; re-read each shot prompt |
| Shot 2 looks like a different video | the style lock pasted word for word, not paraphrased |
| One prompt asked for many fast cuts | per-shot prompts and a cut list |
| Hex or numbers that are not in the frames | only values you read or measured; the rest go under gaps |
| Quality-word padding ("8K, masterpiece") | at most one short quality clause; every clause describes something visible |

---

## Remix

Keep the reference's idea and structure; swap in a new product or brand. Two deliveries in two
turns: the reference prompt, then the final prompt.

### When to use it

Trigger phrases: "same idea as this video", "remake this for my product", "adapt this ad to my
brand", "regenerate this video", "time sequence prompt", "timestamp prompt", "beat prompt", "remix
this".

### Extra input to ask for

Turn order is fixed; each arrow is a turn boundary:

```text
ask for the video -> analyse -> REFERENCE PROMPT -> ask for the product -> adapt -> FINAL PROMPT
```

- No video yet: ask for it and nothing else.
- After the reference prompt, ask in one message: "Share the product image or link you want this
  recreated for. The image is best for getting the pack right. Also confirm: keep [aspect] and
  [duration]?" Put in the reference's real aspect and duration. Confirming aspect is a standing
  rule.
- If the video and product arrive together, still deliver the reference prompt first, then the
  final prompt in the same reply, clearly separated.
- Talking-head references: ask for the script or transcript before writing dialogue beats (or
  switch to [UGC + script](#ugc--script)).

### What changes vs the base method

**Step 4 (audio): find the hits.** Besides the base passes, momentary loudness every 0.1 s shows
hits and drops:

```bash
ffmpeg -hide_banner -i "$V" -af ebur128 -f null - 2>&1 | grep -E "^\[Parsed_ebur128.*M:" > loudness.txt
```

A jump in `M:` usually marks an impact or a cut. A drop just before a jump usually marks a musical
pause before a reveal. Keep that pause and hit in the remix.

**Step 5c (whole piece): name the structure type first.** It decides the output shape.

| Type | Signs | Lock |
|---|---|---|
| One-take morph | one continuous shot; the world transforms around a fixed subject | the subject's position and size in frame |
| Beat-cut edit | hard cuts on the music, many short shots | set, lens and light; arrangement and effects vary per shot |
| Talking head / UGC | a person on camera, speech-driven | use [UGC + script](#ugc--script) |
| Hybrid | segments of the above | say which segment is which |

Also list: what is locked and what varies; the two or three **signature devices** that make the
video memorable; and any source brand, logo or legible signage.

Cut detection is only a candidate list. Fast motion in a one-take fires false cuts; morphs and
whip pans often fire none. Read beat boundaries from the timestamped frames. If the filename says
something different from what is on screen, trust the frames and say so in one line.

**Step 6 (briefs): split image and video, and follow the remix rules.**

1. **Start-frame image prompt** (one per distinct arrangement). Six parts in one prose paragraph:
   `[subject] in [environment], [camera angle or framing], [light source and direction], [mood], [visual style].`
   Product look, set, light and grade live here and only here. Label four **locked constants**
   (Subject, Environment, Lighting, Style) and paste them unchanged into every variant. Only camera,
   arrangement and mood vary. Even a changed adjective shifts the render.
   - One-take morph: one start frame.
   - Beat-cut edit: a clean set plate, then one variant per distinct product arrangement.
2. **Video time-sequence prompt.** Motion, camera, timing and sound only. One header line points at
   the start frame; after that the product is a short handle ("the can", "the tube"). Never
   re-describe the product or set; that invites the model to redraw it and drift. Layout:

   ```text
   AI Video Prompt - "Title" (Ns time sequence, 9:16)
   Start frame: use the attached start image; keep the product exactly as shown.
   Style: [motion character only, e.g. high-speed liquid physics, slow-motion peaks]
   Continuity rule / Edit rule: [e.g. hard cuts on the music beat; set and light never change]
   Tone: a -> b -> c

   0:00 - 0:03 (Beat name)
   Shot: [size and move]
   [action lines]
   SFX: [...]

   Avoid: [general failure modes only]
   ```

   Timestamps and labelled shots are honoured differently per model. On Seedance 2.0 they are hints
   inside labelled shots (see `../models/seedance.md`); syntax may differ by provider.
3. **Rules each prompt is checked against:**
   - **The model draws the nouns it reads.** "Avoid: people, straws" can add people and straws.
     State exclusions positively inside the beat ("the ledge holds only the two cans"). The Avoid
     line names no objects, people or brands: `warping, melting or morphing of the product,
     flicker, garbled or unreadable text, jittery motion, plastic CGI look, oversaturated
     highlights, inconsistent scale between shots`. Never write the source brand, not even "no
     [brand] logo".
   - **Every effect has a physical cause.** Not "lime wheels float around the can" but "the splash
     throws lime wheels upward and they spin as they fall back past it". Every transition has a
     carrier: "the snow spray thickens into ocean spray". Light has a source: "hard sun from high
     behind the bottles", not "glowing".
   - **Beat density.** About one main action plus one secondary motion per second. A sub-second
     beat gets one action. Complex actions get sub-times inside the beat. A finale has at most three
     hero elements, with particles as a fourth. More than about five worlds or twelve cuts in under
     10 s: split into clips.
   - **No device words in action lines.** Never "phone", "lens" (as in "close to the lens"), "rig",
     "tripod", "selfie stick", "a few cm from the camera". The model may draw the device. Camera
     verbs in the `Shot:` line are fine. Lens character goes in the image prompt as a look
     ("ultra-wide 14mm perspective with slight barrel distortion"). Keep mirrors, glossy cans and
     car windows angled away or matte so they do not reflect a camera.
   - **Sequence grammar.** Two similar static shots in a row read as a jump cut; make each change
     physically distinct (wide to close, low to overhead). In a one-take, state the subject's
     position and size as the continuity rule. Over-the-shoulder and look-back shots read as
     cinematic; keep them out of UGC.
   - **UGC vs cinematic grammar.** Cinematic allows stylised motivated light, rim light, flares,
     slow motion, fog, god rays, effects. UGC anchors light to sources in the room (a window to her
     left), no ring light, fog or perfect symmetry, natural handheld framing.
4. **Reference prompt only:** describe the source product generically (type, shape, colours,
   finish), never its name, logo or signature mark. Make background branding generic or defocused.
   Say so in one line.

**New step between 6 and 7: product intake.**

- **Image supplied:** record shape, material, colours, cap or closure, how it stands, wordmark and
  its position, variant, visible claims. Check the label for typos; AI-made product renders often
  have them, and the reference image repeats them in every frame. Flag a typo at the top of the
  final reply.
- **Link supplied:** fetch it. App-shell and quick-commerce pages often come back empty; then search
  the product name for its copy on other retailers or the brand site. Text gives claims, not pack
  visuals. With no image, write the product block with an `[ADD: colours, wordmark, artwork]` slot
  and say an image would lock the pack. Never invent pack colours.
- List the product's **claims and sensory cues** (flavour, ingredients, benefits, texture, usage
  moment). They drive the adaptation.
- Regulated or time-sensitive claims (health, SPF, "zero", caffeine amounts) get a pre-launch
  verification flag. Claim copy goes on an end card in the edit, never in the generation prompt.
- If the user's product is a third-party brand they may not own, do not block. Say once that
  publishing brand content usually needs the brand's approval.

**Adaptation.** Keep the structure type, the beat grid (same timestamps, so the edit rhythm is
reusable), the signature devices and the energy curve. Answer each:

| Source element | Question |
|---|---|
| Product and its form | How does the new product stand, open and catch light? A tube stands on its cap; a can pops a tab; a clear bottle glows with liquid; aluminium only glints. |
| Worlds and effects | Which claim or ingredient can each beat show? One claim per world where possible. |
| Signature device | Is there a brand-native equivalent? |
| Setting | Does it fit the brand's market, or does it need a local equivalent? |
| Tone and physics | Does the category tolerate the reference's force? Luxury skincare does not crack asphalt; it lands in a sand burst. |
| Ending | Does it end on a clean hero moment? Plan an end card in the edit if the reference has none. |

Timing defaults: the source's own beat grid. Building a 15 s ad from scratch: 0 to 3 s setup, 3 to
7 s action, 7 to 12 s escalation, 12 to 15 s hero moment. Slow motion for impact moments only, then
back to speed. Keep the source's audio arc: a pause or drop before the reveal, then a hit.
Voiceover for a text-to-speech tool: write numbers out ("two point five"); about 90 to 100 words
per 30 s.

**Step 7 (deliver): two deliveries.**

- Reference prompt: one or two lines of format and structure type (and "the source brand is
  described generically"); start-frame prompts with labelled constants; the time-sequence prompt
  with every beat at its real timestamp; a clip-split note if needed; then the product ask. Nothing
  after the ask.
- Final prompt: flags (label typo, IP, claim checks), one line each, only if any; the concept in two
  or three sentences (what is kept, what is swapped, why); **A.** start frames; **B.** time-sequence
  prompt, one code block per clip; **C.** production plan: clips and lengths, start-frame chaining
  (last frame of clip N starts clip N+1), the source's cut timestamps for snapping the edit to a
  similar-tempo track, end-card copy, flags. Each prompt in its own code block. At most one question.
- Another product on the same reference later: reuse the reference prompt; rerun intake, adaptation
  and delivery only.

### Output format, filled (final prompt excerpt)

A beat-cut reference (low-angle ledge, two cans, fruit splashes on the beat) adapted to a fictional
ginger-lime sparkling water in a slim can. The user supplied a pack image.

**Concept:** keeps the reference's 6.3 s beat-cut grid and its locked low-angle set. The fruit
becomes ginger and lime; the reference's arc of falling fruit becomes an arc of fizz carrying thin
ginger slices. The seaside town becomes a sunlit rooftop terrace to fit the brand's city audience.

```text
LOCKED CONSTANTS
Subject: a 330ml slim aluminium can, pale mint body, white wordmark running vertically up the front, a ginger-root illustration below it, as in the attached pack image; ice-cold and beaded with condensation, standing upright
Environment: a weathered pale-stone parapet ledge with a rough pitted texture filling the bottom third of the frame; behind it, softly blurred, a rooftop terrace with potted olive trees and a white rendered wall under a deep cobalt sky
Lighting: hard midday sun from high behind the cans, rim-lighting their edges, sparkling on the condensation, short crisp shadows on the stone
Style: hyper-real commercial product photography, punchy saturated colour, polarised sky, crisp detail

Frame 1 - Twin cans: Two cans stand side by side at the centre of the ledge, an olive tree between and behind them. [Environment]. Low hero angle at ledge level with an ultra-wide 14mm perspective and slight barrel distortion, the stone sharp in the foreground. [Lighting]. Fresh, bright, energetic mood. [Style].
```

```text
AI Video Prompt - "Ginger Fizz Burst" Clip 1 (0:00-0:02.1, 9:16)
Start frame: use the attached Frame 1; keep both cans exactly as shown.
Style: high-speed liquid physics, slow-motion peaks, sharp beat-synced cuts
Edit rule: hard cuts on the music beat; set and light never change
Tone: fresh -> explosive

0:00 - 0:00.8 (Twin tab pop)
Shot: static low wide
Both pull tabs snap open together and pressurised fizz sprays straight up from the openings in two twisting ribbons, then falls back down.
SFX: sharp double can-crack and hiss as the music kicks in

0:00.8 - 0:01.4 (Lime crown)
Shot: hard cut, quick punch-in
A lime half dropped from above hits the ledge between the cans and throws up a crown of fizz; the splash flings lime wheels outward in slow-motion arcs. The ledge holds only the two cans and the fruit.
SFX: heavy fizzy splash

0:01.4 - 0:02.1 (Ginger arc)
Shot: cut to a slightly wider frame, one can centred
A burst of fizz from the ledge behind the can tosses thin ginger slices upward; they spin in a loose arc over its top and fall back past it, droplets glinting.
SFX: airy whoosh, soft fizz sparkle

Avoid: warping or morphing of the can, flicker, garbled text, jittery motion, plastic CGI look, inconsistent scale between cuts
```

Production plan (excerpt): generate the clean set plate, then Frames 1 to 6 from it with the pack
image attached. Clip 1 covers 0:00 to 2.1 s; generate at the model's minimum length and trim to the
beat; its last frame starts Clip 2. Source cut points: 0.8, 1.4, 2.1, 2.7, 3.3, 3.9, 4.5, 4.8, 5.1,
5.4, 5.6 s. End card in the edit: the sealed can on the ledge with the user's claim line as a text
overlay; verify the claim before launch.

Why it works: every effect has a cause (tabs open, a dropped lime, a fizz burst); the only
exclusion is positive and inside its beat; the Avoid line names no objects; each sub-second beat
has one action; no device words; the product is only "the can" in the video prompt.

### Pitfalls → fixes

Diagnose a failed generation by its physical cause before rewriting.

| Symptom | Likely cause | Fix |
|---|---|---|
| Unwanted object appears | a noun in the prompt, often in Avoid | remove the noun; state the positive inside the beat |
| Product drifts or morphs | the video prompt re-describes it, or no reference image | strip the description; attach the pack image; add a continuity rule |
| Effect looks random | no physical cause | name the source and the carrier |
| Actions skipped or smeared | beat overloaded | cut actions, add sub-times, or split the clip |
| Camera or phone visible | device words, or a reflective surface | remove device words; angle or matte the surfaces |
| Generic look | weak subject or environment | add specific story detail to the image prompt |
| Fake or plastic look | over-polished style words, unmotivated light | add realism cues; name the light source |
| Jump-cut feel | two similar static shots in a row | make the angle or size change physically distinct |
| Product talk before the reference prompt | steps merged | reference prompt first, product ask last |
| Pack colours guessed from a link | no image | `[ADD: ...]` slot and ask for the image |
| Label typo in every frame | typo in the pack render | flag it before generating |

---

## UGC + script

A reference UGC clip sets how it looks; the user's script sets what is said. Merge them into one
prompt for an avatar or talking-head generator. This is a converter, not a creative job: when in
doubt, pick the option closest to the reference.

### When to use it

Trigger phrases: "recreate this UGC with my script", "same video, my script", "make the avatar say
this like in this video", "UGC ka prompt bana do", or a dropped talking-head video plus a pasted
script. Not for inventing UGC concepts or writing scripts; use
[../use-cases/talking-head-ugc.md](../use-cases/talking-head-ugc.md) for that.

### Extra input to ask for

- **Required:** the reference video and the script. If either is missing, ask for it in one short
  message and stop.
- **Optional:** a target duration or scene structure (it overrides the reference's timing); assets
  (product image, avatar image, logo, app screenshot), used exactly as supplied.
- Nothing else up front. Fill small gaps with the plainest assumption and list it at the end.

### What changes vs the base method

**Step 1:** a screen recording of a phone playing the video is common. Ignore the phone and app UI
(status bar, buttons, app captions, progress bar) and describe only the video inside it, unless the
user wants that UI recreated.

**Step 3 (frames): read framing and camera the UGC way.**

- **Framing from face height** (face top to chin, as a percent of frame height):

  | Face height | Shot size |
  |---|---|
  | 40% or more | extreme close-up / tight close-up |
  | 22% to 40% | close-up (head and top of shoulders) |
  | 13% to 22% | medium close-up (head to chest) |
  | 7% to 13% | medium (head to waist) |
  | under 7% | wide / full body |
  | no face | product shot, hands only, screen, or face turned away |

- Note face placement (left third, centred, right third), eye-line height and headroom.
- **Camera:** the key call is static vs natural handheld sway. Selfie = arm's length, slightly high,
  slight wide-angle distortion. Propped = level and steady. A real move is rare; if present, note
  direction and rough amount, and check whether the person or the camera moves.
- Use a Step 3 strip across any gesture or product reveal to see how it unfolds.

**Step 4 (audio):** the reference's words are replaced, so its transcript only gives pacing, pauses
and where the hook, product and CTA lines sit. Keep music only if the reference has it.

**Step 5b (per shot): record these, from the frames only.** Posture; head movement; gesture
frequency (rare, occasional, frequent) and which hand; facial energy; eye contact (lens, product,
off-camera); product in or out, which hand, height (face, chest, waist), size as a fraction of frame
height, label facing camera or not, when it enters and leaves; 2 or 3 background elements with
positions; depth of field; main light direction. Avatar described generically (age range,
wardrobe, hair); never name or identify a real person. Anything you cannot see is "unclear" and
becomes an assumption, not an invention.

**Step 6 (briefs): lock the script and map it to scenes, instead of briefs per shot.**

1. **Script verbatim:** same words, order and punctuation. No grammar fixes, trims, filler or
   translation unless the user asks. If a line has the avatar claim personal results, flag it under
   the honesty rules in [../use-cases/talking-head-ugc.md](../use-cases/talking-head-ugc.md)
   section 7; do not rewrite it silently.
2. **Timing:** about 2.5 words per second (range 2.2 to 2.8) plus about 0.3 s per scene to settle
   before and land after. If the script misses the target duration by more than about 15%, keep the
   script and tell the user the realistic length.
3. **Scene mapping, in priority order:**
   1. A user-given structure or duration wins.
   2. Otherwise match the reference's shot count and shot types, and give lines to shots by job:
      hook to the opening shot, product lines to the shot that shows the product, CTA to the close.
   3. If the script is much longer or shorter, keep the reference's pattern (close-up talking, then
      medium with product, then close-up CTA) and stretch or compress it. Repeat an existing shot
      type; never invent a new one.
   4. Split only at sentence or clause boundaries.
   5. Scenes about 2 to 8 s each, summing to the total. Hard cuts unless the reference clearly uses
      something else.
4. **Writing rules:**
   - Describe only what the reference shows or the user asked for. No added B-roll, extra people,
     captions, graphics, transitions, zooms or effects. Do not hint at "dynamic" content.
   - Camera: "static camera" for propped, or "handheld selfie framing with only subtle natural sway,
     no deliberate camera moves". Describe a real move once, plainly, with direction.
   - One or two gestures per scene, written next to the phrase they belong to; otherwise the avatar
     is relaxed. The tested finding in talking-head-ugc.md holds: a gesture lands on its own timing,
     not on the word, so never plan an edit card on the word. Moderate expressions; mention blinks
     and micro-pauses instead of more movement. Avoid "energetic", "animated", "dramatic",
     "expressive" unless the reference shows that energy; models overdo them.
   - Product and assets: "the provided product image, reproduced exactly as supplied". State only
     position, size in frame, hand and orientation. If the reference shows another brand's product,
     put the user's asset in the same place and size and never name the reference brand.
   - Continuity once in the global block; scene blocks never contradict it. Keep any outfit or
     location change the reference has and say so in that scene.
   - Concrete over adjectives: "medium close-up, head and shoulders, face centred slightly above
     middle, eye level, about arm's length away" reproduces; "engaging authentic shot" does not.
   - Left and right from the viewer's side, checked against the frames.
   - Prompt in English unless asked; the script stays in its own language.
5. **Route:** `avatar-talking-head` or `dialogue-lipsync` in `../model-router.md`. Reuse the voice
   block and line-sizing table from talking-head-ugc.md. If the user names a generator with its own
   format (character limit, timestamp syntax), adapt to it; model-native syntax may differ by
   provider.

**Step 7 (deliver):** the whole prompt in one fenced block. Below it, a few short lines: total
duration, scene count, and **Assumptions** (real ones only, one line each). If the generator caps
clips shorter than the total (many cap at 5 to 10 s), also give each scene as a standalone prompt
that repeats the global block, to generate clip by clip and join with hard cuts. Offer the biggest
lever in one line: the first keyframe or the user's avatar image as the start frame, and the
product image attached directly.

**Revisions:** change only the part asked for ("make scene 2 a medium shot") and return the full
updated prompt. Do not reinterpret untouched scenes.

**Quality gate (fix silently, do not report):** script matches character for character, in order;
durations sum to the total and each line fits at about 2.5 words per second; every scene has
framing, position, action, expression, dialogue, duration and cut type; nothing the reference does
not show; gestures sparse; product wording says "exactly as supplied" and covers only position,
size, hand and orientation; left and right checked; no clash between global and scene blocks.

### Output format, filled

Reference: 14 s vertical selfie video, man about 30 to 35, navy crew-neck t-shirt, kitchen with
white tiles and a shelf of jars behind his left shoulder, soft window light from frame right. Two
hard cuts: close-up talking (0 to 4 s), medium close-up holding a bottle at chest height in his
right hand (4 to 11 s), close-up again (11 to 14 s). Handheld, slight sway. No captions, no music.
Asset: the user's water bottle image.

Script (user-supplied, 30 words): "This is the bottle I keep seeing everywhere. It's light, the lid
opens with one hand, and it keeps water cold for twelve hours. Link's below if you want one."

Fit: scene 1, 8 words, about 3.5 s in 4 s; scene 2, 16 words, about 6.7 s in 7 s; scene 3, 6 words,
about 2.7 s in 3 s.

```text
UGC VIDEO - 14s, 9:16 vertical, 3 scenes, hard cuts only

GLOBAL (applies to every scene)
Format: 9:16, 14 seconds, phone-shot selfie UGC look, natural colors, no filters.
Avatar: man in his early 30s, short dark hair, light stubble, navy crew-neck t-shirt. Same person, outfit and hair in every scene.
Environment: kitchen, white square wall tiles behind him, a wooden shelf of glass jars behind his left shoulder (frame right), softly out of focus. Unchanged across scenes.
Camera: front-facing, held at arm's length, eye level, slightly above. Handheld with only subtle natural sway. No zooms, pans, tilts or deliberate camera moves.
Lighting: soft daylight from a window at frame right, gentle shadow on the frame-left side of his face, neutral. Consistent across scenes.
Product: water bottle - use the provided product image exactly as supplied; do not redesign, recolor, restyle or reinterpret it.
Delivery: speaks directly to the viewer in a relaxed, friendly, conversational tone, natural pace, natural blinking and small pauses. Gestures only on the moments noted below; otherwise hands relaxed and still. Moderate, genuine facial expressions.
Audio: his voice only, clean room tone, no music.

SCENE 1 - 0.0-4.0s - Close-up
Position: head and top of shoulders, face centred, eyes about one third from the top of frame, small headroom.
Action: slight lean in on "This is the bottle"; otherwise still.
Expression: easy half-smile, eyebrows lift a little on "everywhere".
Dialogue: "This is the bottle I keep seeing everywhere."
-> Hard cut

SCENE 2 - 4.0-11.0s - Medium close-up
Position: head to mid-chest, face centred slightly right of middle.
Action: raises the bottle in his right hand (frame left) to chest height on "It's light", holds it steady; small thumb flick at the lid on "opens with one hand".
Expression: relaxed, small nod on "twelve hours".
Product: bottle at chest height, upright, front facing the viewer, about one quarter of frame height. Exactly as supplied.
Dialogue: "It's light, the lid opens with one hand, and it keeps water cold for twelve hours."
Delivery note: brief pause after "It's light".
-> Hard cut

SCENE 3 - 11.0-14.0s - Close-up
Position: same framing as Scene 1, product out of frame.
Action: small nod on "Link's below"; no other gestures.
Expression: warm, genuine smile.
Dialogue: "Link's below if you want one."
Delivery note: unhurried; hold the smile for about a second after the last word.
(End)

AVOID: B-roll, extra people, on-screen text or captions, graphics, transitions other than hard cuts, camera movement, zooms, exaggerated or constant gestures, robotic or jerky head movement, over-animated expressions, lip-sync drift, changes to the avatar, outfit, environment or product between scenes, any alteration of the product's design or label.
```

Assumptions: kept the reference's 3-shot structure and timing; put the product line in the shot
where the reference shows the product; "keeps water cold for twelve hours" is the user's claim,
spoken as written.

Adjust the AVOID line to the reference: if it has captions or a handheld walk, take those items out
of AVOID and describe them in their scene. On models that draw named nouns (see Remix rules), keep
AVOID to failure modes and move object exclusions into the scenes as positive statements.

### Pitfalls → fixes

| Pitfall | Fix |
|---|---|
| Script "improved" or trimmed | paste it verbatim; tell the user the real duration instead |
| Line does not fit its scene | 2.5 words per second + 0.3 s; move the scene boundary to a clause break |
| Sentence split across two scenes | split only at sentence or clause boundaries |
| Model adds B-roll, captions or zooms | describe only what the reference shows; no "dynamic" hints; list them in AVOID |
| Over-acted, flailing hands | one or two gestures per scene; drop "energetic", "animated", "expressive" |
| Gesture misses its word | expected: it lands on its own timing; place edit cards where it lands |
| Product redrawn or restyled | "exactly as supplied"; only position, size, hand, orientation; attach the image |
| Reference brand leaks in | swap in the user's asset at the same spot; never name the reference brand |
| Hand or side flipped | viewer's left and right, checked on the frames |
| Scene blocks contradict the global block | constants live in GLOBAL only; scenes state what is specific |
| Generator caps clip length | per-scene standalone prompts with GLOBAL repeated, joined with hard cuts |
| Revision rewrites the whole prompt | edit only the named part; return the full prompt |

<!-- Sources: video-replica-prompt (SKILL.md, references/analysis_checklist.md, prompt_writing_guide.md, output_template.md, scripts/compare_videos.py), video-remix-prompt (SKILL.md, references/prompt-rules.md, output-template.md, scripts/analyze_video.py), ugc-video-prompt (SKILL.md, references/observation_checklist.md, output_template.md, scripts/analyze_reference.py); synced claude.ai skills, adapted provider-neutral. Remix and UGC examples rewritten with fictional products. -->
