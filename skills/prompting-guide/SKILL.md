---
name: prompting-guide
description: >-
  The one prompting skill for AI image and video generation, for any provider (an MCP, an API, a
  web UI). Turns an idea, a shot list or a reference video into a director's brief per shot, picks
  the right model family, compiles the brief into that model's own prompt dialect, adds the right
  look blocks (light, Kelvin, lens, film stock, atmosphere, skin and eye realism, reference sheets),
  self-checks every prompt before anything is spent, and routes each request type to a tested
  recipe: avatars and realistic people, talking heads and UGC, character consistency, product
  shots, text / logos / UI, cinematic story shots and transitions, anime / pixel art / sprites,
  ads and promos.
  Use when: writing, fixing or improving any image or video prompt; "write the prompts for these
  shots"; "which model should I use"; "make an avatar / AI twin / headshot"; "the generations look
  generic / fake / plastic"; "keep the character consistent"; "make it look like film"; planning a
  reel, ad or short film shot by shot; "break down this video / recreate this reel as prompts".
  NOT for: running and downloading generations (use the provider's own tools or run skill), the
  creative strategy and claims of an ad, editing or assembling the final video.
---

# Prompting guide

Models do not need a better prompt. They need a director's brief, translated into the dialect each
model actually reads. Veo wants a dense, camera-first scene with labelled sound. LTX wants one
flowing present-tense paragraph. Seedance wants role-tagged references and labelled shots. MiniMax
wants one beat per shot and body language over facial adjectives. FLUX ignores negatives. One
prompt style for all of them wastes money.

This skill is provider-neutral. Model names are families ("Kling 3 Pro", "Seedance 2.0"). Exact
option names, allowed values and prices always come from the provider in use, never from memory.

## Finding a specific part

Do not load whole folders. [INDEX.md](INDEX.md) lists every section of every file with a stable id,
the file and the line. For a narrow question ("Veo dialogue syntax", "Kling first + last frame",
"skin looks plastic", "Kelvin for golden hour"):

1. Check the **Quick lookup** table at the top of INDEX.md.
2. Otherwise search INDEX.md for the keyword (Grep), take the row's file and line, and Read that file
   from that line (offset) for about 60 lines.
3. Cite sections by id (`models.veo.compile`) when you tell another skill or agent where a rule lives.

After editing any file in this skill, run `python scripts/build_index.py` so the line numbers stay
right (`--check` exits 1 when INDEX.md is stale).

## Pick the mode

| The user gives you | Mode |
|---|---|
| An idea, a script, a shot list, or "make me an image / clip of X" | **A. Write** (below) |
| A prompt that failed or "looks generic / fake" | **B. Fix**: run Step 4's self-check on it, read the model file's Failure modes, change one variable, re-check |
| A reference video, reel, ad or image to recreate | **C. Reverse**: [references/reverse/video-to-prompt.md](references/reverse/video-to-prompt.md), then continue at Step 2 here. Variants in [reverse/variants.md](references/reverse/variants.md): **Replica** (copy it exactly), **Remix** (same structure, new product), **UGC + script** (reference performance, new words) |

## Route by request type first

Before writing anything, match the request to a use case and load that file. It says which style
files and shot types to use, with a tested recipe.

| Request sounds like | Load |
|---|---|
| avatar, AI twin, headshot, portrait, realistic person, "looks fake / plastic skin" | [use-cases/avatar-portrait.md](references/use-cases/avatar-portrait.md) |
| talking head, UGC, testimonial, lip-sync, character speaks / voiceover | [use-cases/talking-head-ugc.md](references/use-cases/talking-head-ugc.md) |
| same character across shots, mascot, character sheet, "face keeps changing" | [use-cases/character-consistency.md](references/use-cases/character-consistency.md) |
| product shot, packshot, label, product in motion, plug / lid / key into something | [use-cases/product.md](references/use-cases/product.md) |
| text in the image, logo, poster, thumbnail, UI, app screen, phone screen | [use-cases/text-logo-ui.md](references/use-cases/text-logo-ui.md) |
| cinematic shot, story reel, world still, image-to-video, hidden transition, multi-shot | [use-cases/cinematic-story.md](references/use-cases/cinematic-story.md) |
| anime, illustration, cartoon, pixel art, sprite, game tile, icon set | [use-cases/stylized-anime-pixel.md](references/use-cases/stylized-anime-pixel.md) |
| ad, promo, launch film, SaaS demo, brand film | [use-cases/ads-promo.md](references/use-cases/ads-promo.md) |
| edit this image, change only X, make it winter / night / on fire, restyle a clip | [use-cases/edit-restyle.md](references/use-cases/edit-restyle.md) |

A request can hit two rows (a talking avatar = avatar-portrait + talking-head-ugc). Load both.
No match: use the universal rules and the router alone.

## Mode A: write

Pipeline: **brief → route → compile → look blocks → self-check → price → hand to the run.**
Nothing is generated in this skill.

### Step 1. Write the Director's Brief (model-agnostic)

One brief per shot, schema in [references/brief-schema.md](references/brief-schema.md). For a
one-off image or quick clip, fill only the minimum viable brief (section 5 of that file).

- Write the **cast bible** once: one trait line per character (6 to 10 concrete visible traits),
  one set line, one look line. Shots point at them by id. Paste trait lines word for word.
- One shot = one primary beat. Two beats that need different framing are two shots.
- `used_s` is what the edit keeps; `gen_s` is what you generate (Step 2 sets it).
- Every `avoid` item carries its positive replacement (`red gloves -> both gloves are blue`).
- Mark `audio: none` when sound is added in the edit. Silent generation is often cheaper.

### Step 2. Route each shot

Open [references/model-router.md](references/model-router.md). From the shot type, the inputs it
needs (first frame, last frame, identity refs, audio ref), priority and budget, pick default /
cheap draft / premium. Then, with the provider in use:

1. List the provider's models once per session; confirm the pick exists there.
2. Read the picked model's options once; write the exact option names and allowed values next to
   the shot. Every setting you send must come from that list.
3. Set `gen_s`: the smallest allowed duration that is >= `used_s` + 1.5 s (last frames can break).

No tool to list models (a web UI, a pasted request)? Say which family you picked and why, and give
the settings as plain labels for the user to set.

### Step 3. Compile

Open the model family's file from the router's table, and only that one. Apply its **Compile**
section: slot order, length band, timing syntax, reference syntax, audio syntax, what to drop
because a reference already carries it, and the settings mapping.

### Step 4. Look blocks

For any named look, load the matching file via [references/styles/README.md](references/styles/README.md)
and paste its block into the light / lens / motion / film / look slot: light direction, Kelvin
colour temperature, aperture and focus, shutter and motion blur, film stock, atmosphere (haze,
dust, embers, backlit rain), skin and eye realism, character or prop reference sheets. Model syntax
comes from the model file; look wording comes from the style file. The same look line goes word for
word into every shot. **Any shot with a realistic human face gets the realism block.**

### Step 5. Self-check before anything is spent (mandatory)

Run this critique on every compiled prompt, then the model file's own Self-check list. Write
`check: PASS` or the failed items plus the fix. Rewrite and re-check, at most 2 rounds. A prompt
that still fails goes to the user, not to the model.

1. **Brief coverage:** subject (trait line verbatim), the one primary beat with an endpoint, camera
   (one move with start and end, or "static"), a light source, the look line.
2. **Dialect:** the model file's slot order, length band and timing syntax. Count words.
3. **References:** list order equals the numbering in the prompt; each reference has one stated
   role; a first-frame shot does not re-describe the frame.
4. **Contradictions:** nothing the first or last frame already contradicts; never a camera move and
   "static" together.
5. **Avoid list:** each item became a positive statement or an allowed constraint line; no booster
   words (stunning, epic, masterpiece, 8K, a lone "cinematic").
6. **Known failure modes:** if the shot hits one in the model file's table, apply the fix or re-route.
7. **Settings:** every option and value exists for this model at this provider; audio matches the
   brief; aspect and duration are allowed values; no locked option is overridden.

### Step 6. Price, then hand off

If the provider can quote a price, get it per shot with the exact settings, sum the job, and add 2
retakes for each `priority: hero` shot. If the total is large for this user, show the shot table
(shot, model, why, price) and wait for a yes; otherwise state the total in one line and go.

Hand the compiled prompts and settings to whatever runs the generation. Do not rewrite prompts
during the run. If a take fails, come back here, change one brief field, recompile, re-check.

## Universal rules (every model)

1. **Order is priority.** `Subject + Action + Setting + Camera + Light + Style + Sound + Constraints`.
   Skip any slot a reference already carries.
2. **Name the subject, never pronoun it.** In multi-character shots give each person one distinct
   visual tag and reuse it every time.
3. **One visible beat with an endpoint.** Actor + verb + timing + result. More beats = more shots.
4. **Film language, one camera move per shot**, with start and end framing. Shot size, angle, lens.
   No camera line = random framing. Static gets one sentence.
5. **Light from physical sources**, not moods: direction, colour, time of day, haze.
6. **Dense style labels, no empty boosters.** Media and movement names that pull a clear look.
   Resolution is a setting, not a word. "Slightly grainy, film-like" fights the over-clean AI look.
7. **Describe what IS there.** Naming a flaw plants it. Keep literal negation to short constraint
   lines the model expects. Use a negative-prompt field only if the model offers one.
8. **Aspect ratio up front**, chosen from the destination (9:16 reels, 1:1 / 4:5 feed, 16:9 web,
   21:9 cinematic); compose for it in words too.
9. **Reference order is numbering.** Item 1 in the reference list is "image 1" in the prose. One job
   per reference; say what must NOT transfer; with a reference, prompt only what it cannot show.
10. **Multi-shot:** labelled shots with timecodes, about 4 to 6 s each, name the transition; for one
    take say "single continuous take, no cuts". Repeat character tag and look line every shot.
11. **Text:** exact words in double quotes, few words, placement and size. Video models garble UI:
    screens get "even cool white glow" and real content goes in during editing.
12. **Character consistency:** a reference image on every shot plus the fixed trait line, word for
    word. Faces that act need at least a medium close-up. Re-anchor to the ORIGINAL reference when
    a chain drifts.
13. **Sound (native-audio models):** name all four layers: dialogue, ambience, effects, music (or
    "no music"). Dialogue after a colon, "(no subtitles)", 2 to 3 short sentences per 8 s.
14. **Iterate one variable at a time.** Before calling something impossible, try another take, a
    shorter duration and a simpler shot.
15. **Object into object: lock the end state.** Name the real part and its size against its mate,
    make start and end keyframes, check the end keyframe, animate between them.

## Rules for working

- Discover, never recall: model availability, option names and prices come from the provider.
- One model per shot on purpose. Draft on the cheap column, then promote the winning prompt.
- Variety comes from changing the prompt; most providers expose no seed.
- Talk to the user like a director: what each shot is for, which model and why in a few words,
  the price. No internal ids unless asked.

## Files

| Folder | What is in it |
|---|---|
| `INDEX.md` | Every section, by id, file and line; quick lookups first |
| `scripts/build_index.py` | Regenerates INDEX.md after edits |
| `references/brief-schema.md` | Director's Brief schema, field meanings, shot types |
| `references/model-router.md` | Shot type → model family, and family → file |
| `references/models/` | One file per model family: Compile, Self-check, Failure modes, Field notes |
| `references/styles/` | Look blocks; start at `README.md` |
| `references/use-cases/` | Recipes per request type (table above) |
| `references/reverse/` | Reference video or image → prompts, with the breakdown template |
