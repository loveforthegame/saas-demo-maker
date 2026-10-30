# Reverse mode: video or image to prompts

Turn a reference video (or one still) into a breakdown someone could reshoot from, then into one
Director's Brief per shot (`../brief-schema.md`). The briefs are model-agnostic. Compile each shot
with the matching `../models/<family>.md` file via `../model-router.md`, then run it with whatever
provider the user has.

Default output: the breakdown plus the briefs and compiled prompts. Generate nothing unless the
user asks.

## Pick the variant

Run this method for every reference video. If the ask matches a row, also apply that variant's
changes from [variants.md](variants.md).

| The user wants | Variant |
|---|---|
| the same video as closely as possible ("copy this", "replicate", "ditto copy") | [Replica](variants.md#replica) |
| the same idea and structure for a new product or brand ("same idea as this", "time sequence prompt") | [Remix](variants.md#remix) |
| the reference's performance with new words from their script ("recreate this UGC with my script") | [UGC + script](variants.md#ugc--script) |
| a breakdown and briefs to reshoot with their own cast | none: this file as written |

## What you can and cannot perceive

- You see stills you extract, not motion. Infer motion from consecutive frames and say when
  something is inferred.
- You do not hear the audio yourself. With the watch skill's `--audio` pass you get measurements
  (times, levels, loudness, sync to cuts) and hints (event tags, music mood). Without it you get
  only loudness and silence data from ffmpeg. Say which one you had in the audio section.
- Words come only from a transcript (captions or speech-to-text). The sound timeline does not
  hear words.
- Burned-in captions you read on frames are on-screen text, not a transcript of the audio. Say
  which is which.
- Never invent details between frames. If a moment matters and you have no frame for it, grab one.

## Step 1: get the file

Check tools first: `ffmpeg -version` and `ffprobe -version`. Missing: stop and give the install
line (`winget install ffmpeg` on Windows, `brew install ffmpeg` on macOS, the package manager on
Linux).

| Source | How |
|---|---|
| Local path | use it; quote paths with spaces |
| Public link (Reels, TikTok, YouTube, X, direct mp4) | `yt-dlp -f "mp4/best" -o "<work>/source.%(ext)s" "<url>"` if `yt-dlp` is installed; direct mp4: `curl -L -o "<work>/source.mp4" "<url>"`; otherwise ask the user to download it. If you use `/watch` in Step 4, it downloads the file for you and its report names the local media path. |
| Earlier generation output | download its output link with `curl -L -o` |
| Pasted into chat, no path | look in Downloads and Desktop for the newest video from the last 15 minutes and show the user the filename; use it only after a yes |

Work folder: `./reverse/<job-slug>/` with `frames/`, `scenes/`, `sheets/`, `strips/` inside.

Only analyse footage the user owns or has a right to study. For a remake, the output is an
original reshoot: keep structure, pacing, framing and light; replace the original's people,
brands, logos and music with the user's own or original ones.

## Step 2: probe

Run all commands in this file from Git Bash on Windows (or any POSIX shell). They also work in
PowerShell except the lines that pipe into `grep`; there, replace `| grep -E "a|b"` with
`| Select-String "a|b"`, and set the variable with `$V = "..."` instead of `V="..."`.

```bash
V="<work>/source.mp4"
ffprobe -v error -show_entries format=duration,size,bit_rate:stream=codec_type,codec_name,width,height,r_frame_rate -of json "$V"
```

Record: duration, resolution and aspect (9:16, 1:1, 16:9), fps, audio stream yes or no.
Long video (over 90 s): ask which part matters, or analyse the first 60 s plus any part the user
names.

## Step 3: extract frames at the beats

Run all four. Scene cuts give the edit, 1 fps gives the in-shot motion, contact sheets keep the
reading cheap, first and last frames anchor the open and close.

```bash
cd "<work>"
# a) Cuts: one frame at each scene change, with its timestamp
ffmpeg -hide_banner -i "$V" -vf "select='gt(scene,0.3)',showinfo" -fps_mode vfr scenes/cut-%03d.jpg 2> scenes/log.txt
grep -o "pts_time:[0-9.]*" scenes/log.txt > scenes/times.txt

# b) Fallback timeline: 1 frame per second (use fps=2 for clips under 10 s)
ffmpeg -hide_banner -loglevel error -i "$V" -vf "fps=1,scale=720:-2" frames/f-%03d.jpg

# c) Contact sheets: 16 frames per image, for a fast first pass
ffmpeg -hide_banner -loglevel error -i "$V" -vf "fps=1,scale=320:-2,tile=4x4" sheets/sheet-%02d.jpg

# d) First and last frame
ffmpeg -hide_banner -loglevel error -i "$V" -frames:v 1 frames/first.jpg
ffmpeg -hide_banner -loglevel error -sseof -0.1 -i "$V" -frames:v 1 frames/last.jpg
```

- `-fps_mode` needs ffmpeg 5.1 or newer. On an older build use `-vsync vfr` instead.
- `scenes/times.txt` empty, or only a couple of cuts in a fast edit: lower the threshold to 0.2.
  Dozens of false cuts (flashes, handheld): raise it to 0.4.
- Frame `f-NNN.jpg` is at about second NNN-1 at 1 fps.
- A precise moment: `ffmpeg -ss <seconds> -i "$V" -frames:v 1 frames/at-<seconds>.jpg`.
- A fast moment the 1 fps frames skip (a hit, a flip, a flash): make a strip of 12 frames across
  one second, centred on it. Set `S` to the moment minus 0.5 s:

  ```bash
  ffmpeg -hide_banner -loglevel error -ss <S> -t 1 -i "$V" -vf "fps=12,scale=240:-2,tile=12x1" -frames:v 1 strips/moment-<t>.jpg
  ```

Read the contact sheets first to map the whole piece. Then read each cut frame, the 1 fps frames
inside any shot that moves or matters, and every strip. Stop once each shot has a start, middle
and end frame.

## Step 4: audio evidence

Skip this step if the probe found no audio stream, and say so.

### Preferred: the watch skill with `--audio`

If the watch skill is installed, run `/watch <source> --audio` (local path or link). `--audio`
forces the local engine, so you get your own evidence, not another model's summary:

- timestamped frames (scene-aware, capped; add `--timestamps T1,T2,...` to pin frames at moments
  you care about, `--resolution 1024` when on-screen text is small, `--start`/`--end` for a long
  source);
- a speech transcript: native captions first, else local WhisperX (or the cloud backend the user
  configured);
- the earshot sound pass, under `## Audio (earshot, local)` in the report: sound events with times
  and levels, music sections, loudness (LUFS), a beat grid, sync of sound to the picture cuts, and
  a sound sheet PNG. Read the PNG with the frames.

How far to trust it:

| Reliable (measurements) | Hints only |
|---|---|
| when a sound starts and stops | the tag on an event in a busy mix ("whoosh", "impact") |
| levels and loudness, silences, loudness jumps | music mood or genre |
| beat grid and tempo | what instrument is playing |
| which cuts land on a beat or hit, and by how much they miss | |

earshot does not hear words. Words come from the transcript only. If the report lists
`Audio pass: earshot not installed`, tell the user and use the fallback below.

The watch frames are enough to map the piece. Still run Step 3a when you need exact cut times or
start, middle and end frames per shot.

### Fallback: ffmpeg only (no listening)

```bash
ffmpeg -hide_banner -i "$V" -af volumedetect -vn -f null - 2>&1 | grep -E "mean_volume|max_volume"
ffmpeg -hide_banner -i "$V" -af silencedetect=n=-35dB:d=0.4 -vn -f null - 2>&1 | grep -E "silence_(start|end)"
```

- Silences mark beat drops, pauses before a punchline, or cut points. Line them up with the scene
  times.
- Speech: if `whisper` is installed, run
  `ffmpeg -i "$V" -vn -ac 1 -ar 16000 audio.wav` then
  `whisper audio.wav --model small --output_format srt --output_dir .` and use the timestamps.
- If neither is available, ask once: "I can't hear it. What's said, and is there music?" Skip the
  question if the user said audio does not matter.

### Use the audio in the breakdown

- Mark big moments: a loudness jump after a build, a hit, a beat drop. Each one gets its own beat
  line at its exact time, and a strip from Step 3 if no frame shows it.
- Note which cuts land on the beat. That becomes the cut rhythm in the pacing section.
- Music nobody in the clip sings or talks to: write that in the shot's `audio` field ("nobody in the
  video sings or talks"), or a model with native audio may move mouths to the music.

## Step 5: analyse in layers

### 5a. Layer map first

The layer decides what gets generated and what gets rebuilt in the edit.

| Layer | Signs | Rebuild with |
|---|---|---|
| Static background / plate | no parallax, still image with slow zoom | an image keyframe, animated with a slow push in the edit or image-to-video |
| Text overlay / captions / stickers | crisp type, pops on cuts, sits over everything | the edit (captions, titles); never ask a video model for it |
| Generated or filmed footage | real motion, camera move, people | one video brief per shot |
| Screen recording / UI | flat, pixel-perfect UI, cursor | the user's own screen capture; a model will garble UI |
| Graphics / B-roll inserts | stock-like clips, product close-ups | a video brief, or a still plus image-to-video |
| Audio | from Step 4 | native-audio model, the user's file, or music added in the edit |

Mark every edit-layer item as EDIT. It never goes in a prompt.

### 5b. Per shot

Timecode in and out, shot size, angle, lens feel, camera move with start and end framing, subject
and action, setting, wardrobe and props, lighting (source, direction, colour), grade and texture,
transition into the next shot, on-screen text verbatim with position, audio at that time.

Write the action as timed beats, one line per moment (`4.0 s: she spins, skirt flares`). Read each
face at each beat and write the expression on that beat line (deadpan, lips parted, closed-mouth
smirk). Expressions belong to beats, never to a character's trait line.

Name the one thing most likely to break in a remake (a tucked shirt, a hand-held prop, a sign's
text). It becomes a constraint repeated at the start and end of that shot's prompt.

### 5c. Whole piece

Hook (first 1 to 3 s), pacing (shot count, average shot length, cut rhythm, where it speeds up),
story arc, recurring motifs, aspect and safe zones for captions.

Full structure: [breakdown-template.md](breakdown-template.md).

## Step 6: write the briefs

Translate the breakdown into the Director's Brief format in `../brief-schema.md`.

1. **Cast bible, once.** One trait line per character: 6 to 10 concrete, visible traits (age,
   build, hair, face marks, garment and colour), taken from the frames or from the user's
   replacement. One set line per location. One look line (grade, grain, lens feel, light style)
   pasted word for word into every shot. Tie each palette hex to an object.
2. **One brief per shot.** Fill from the breakdown:

   | Brief field | Comes from |
   |---|---|
   | `type` | the layer map and the shot's job; the router keys are listed in the schema |
   | `intent` | why the shot is there (the hook, the reveal, the laugh), as a feeling |
   | `beat` | the one thing that changes in the shot |
   | `used_s` | out minus in, from the shot list |
   | `framing` | size, angle, placement, must-be-in-frame items |
   | `camera` | one move, with from and to framing and speed |
   | `lens` | lens feel and depth of field you saw |
   | `motion` | the timed beat lines from 5b, shifted to start at 0 for this shot |
   | `performance` | body-first cues and the per-beat expressions |
   | `lighting` | source, direction, colour |
   | `style` | `look_line`, or a per-shot override |
   | `text_on_screen` | `none` in almost every case; the text goes in the edit |
   | `audio` | dialogue from the transcript, sfx from the sound timeline with times, ambience, music or "no music" |
   | `references` | each with one role: first frame, identity, location, camera and motion (the reference clip), style |
   | `continuity` | the end state the next shot opens on |
   | `avoid` | `problem -> positive replacement`, including the 5b constraint |

3. **Rules that carry over from remake work:**
   - A reference clip, if the target model takes one, carries camera and motion only. Say so in its
     role.
   - Each reference image has one role; everything else about it is ignored.
   - When an image carries a face, give the character a name and a short anchor, not a face
     description. Described faces override the image.
   - Replace the original's people, brands, logos and music. Never copy a real person.
   - Avoid items are positive statements. Many models have no negative field and draw what "no X"
     names.

4. **Compile.** For each brief, pick the model family with `../model-router.md` (by `type`, audio
   need, references and length), then compile with that family's `../models/<family>.md`. Typical
   routing signals from a breakdown:

   | Situation in the reference | Brief `type` to route on |
   |---|---|
   | several short shots, motion-heavy, one look | `multi-shot-sequence` (group 2 or 3 shots per clip) |
   | sync dialogue or native ambience matters | `dialogue-lipsync` or a type with `audio.needed: true` |
   | a look or character must be locked first, or a static plate | `hero-still` / `character-sheet` keyframe, then animate |
   | a text-heavy frame (end card, poster frame) | `text-graphic` for the frame; hold or animate it in the edit |
   | the user has the original clip and wants the same motion with a new look | `restyle` or `motion-transfer` |
   | fast action, one beat | `fast-action` |

   If the user named a model, write for it and note anything it cannot do.

5. **Run.** Hand the compiled prompts to whatever provider the user has. Keyframes first, since
   they are cheap; show them, then the clips from those keyframes. Test one clip before the whole
   set when the job is expensive. To stitch finished clips in shot order, write `list.txt` with
   `file 'clip1.mp4'` lines, then
   `ffmpeg -f concat -safe 0 -i list.txt -c copy reshoot.mp4`
   (re-encode with `-c:v libx264 -c:a aac` if the clips differ in format).

## Step 7: deliver

1. One-line read of the video: what it is and why it works (the hook, the rhythm).
2. The breakdown, in the template format.
3. The cast bible and the shot briefs (YAML).
4. The compiled prompts in fenced `text` blocks, each headed with model family, duration, aspect
   and references needed.
5. An edit list: order, trims, captions, music, end card.
6. One follow-up: "Want me to run shot 1 as a test?"

Keep the work folder. Other steps reuse the frames.

## Quality gate

Before delivering the briefs:

- Every shot in the shot list has a brief, and every brief has `type`, `beat`, `used_s`, framing,
  one camera move, timed motion and an avoid list.
- Every big moment from Step 4 has its own beat line at its time.
- Trait lines and the look line are identical across briefs.
- Nothing from the edit layer (captions, UI, logos) is in a prompt.
- Every audio claim is labelled: measured, hint, transcript, user-said, or unknown.
- No real person, brand or logo from the original is copied.

If the user generated, check the output against the reference. Make side-by-side pairs, one per
second (the reference left, output right):

```bash
ffmpeg -hide_banner -loglevel error -i reference.mp4 -i output.mp4 -filter_complex "[0:v]fps=1,scale=-2:640[a];[1:v]fps=1,scale=-2:640[b];[a][b]hstack" pairs/p-%03d.jpg
```

Give the pairs, the strips, the briefs and the reference images to a fresh reviewer (a new
subagent with no view of what you expect). It returns one line per finding:
`BLOCKER|POLISH, time, what is wrong`.

- **Hard fails:** a generated shot does not match its brief (framing, camera move, action); a beat
  is missing or out of order; timing drifts more than 10% from the breakdown; the constraint broke;
  a melted limb or garbled text stays in frame for more than a few frames.
- **Blocker vs polish:** a blocker is visible at normal speed on a phone and triggers a retake with
  that beat's line changed. Polish is visible only when paused or zoomed; list it, do not retake.
  At most 3 attempts per shot unless the user raises the limit.

## Image to prompt (single still)

Same honesty rules, shorter path.

1. Get the image. Check its size: `ffprobe -v error -show_entries stream=width,height -of csv=p=0 "<image>"`.
   Note the aspect.
2. Read it whole, then crop into the parts that matter (face, hands, product, text) if they are
   small: `ffmpeg -i "<image>" -vf "crop=w:h:x:y" crop-1.png`.
3. Analyse in layers: subject and pose, setting, light (source, direction, hardness, colour),
   lens feel and depth of field, palette, grade and texture, text (verbatim, position, and whether
   it is part of the scene or an overlay for the edit).
4. Write one minimum viable brief (schema section 5): `type` (usually `hero-still`,
   `product-still` or `text-graphic`), `intent`, `beat` (the moment the still captures),
   `framing.size` and angle, `camera.move: static`, `lighting`, `style` (a look line), `aspect`,
   `references` with roles, `audio.needed: false`, `avoid`. Add a cast trait line if a person or
   character must recur.
5. If the user wants the still to move, add a video brief whose first reference is the still with
   role `first_frame`, and describe only motion, camera and sound in it.
6. Compile via `../model-router.md` and the matching `../models/<family>.md`. Deliver the read, the
   brief and the compiled prompt.

<!-- Adapted from MengTo/Skills video-to-superprompt (https://github.com/MengTo/Skills, MIT) -->
