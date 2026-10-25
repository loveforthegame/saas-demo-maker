---
name: predis-director
description: >-
  Turns an idea or a shot list into a Director's Brief per shot, routes each shot to the right
  Predis model, compiles the brief into that model's own prompt dialect and config, critiques every
  compiled prompt against the model's rules, and prices the whole job before a credit is spent.
  Use when: any Predis image or video job with more than a one-line ask; "write the prompts for
  these shots"; "which model should I use for this shot"; "the generations look generic"; planning
  a reel, ad or short film shot by shot; before predis-generate runs anything that costs over
  ~30 credits.
  NOT for: the creative strategy and claims (predis-core:creative-brain); running and downloading
  the generation (predis-core:predis-generate does the run loop); reviewing finished files
  (predis-core:quality-gate).
---

# Predis Director

Models do not need a better prompt. They need a director's brief, translated into the dialect each
model actually reads. Veo wants a dense, camera-first scene with labelled sound. LTX wants one
flowing present-tense paragraph. Seedance wants role-tagged references and labelled shots. MiniMax
wants one beat per shot and body language over facial adjectives. FLUX ignores negatives. One
prompt style for all of them wastes credits.

Pipeline: **brief -> route -> compile -> self-check -> price -> hand to the run loop.** Zero
credits are spent in this skill (only `list_models`, `describe_model`, `estimate_cost`, all free).

Output: `./predis-output/director/<job-slug>/SHOTS.md`, one block per shot: brief, model, config,
compiled prompt, self-check result, price.

## Step 1. Write the Director's Brief (model-agnostic)

Read `./predis-output/brief/<slug>/BRIEF.md` if creative-brain made one. Then fill one brief per
shot with the schema in [references/brief-schema.md](references/brief-schema.md). Rules:

- Write the **cast bible** once (trait line per character, set line, look line). Shots point at it
  by id. The compiler pastes the trait line word for word; you never paraphrase it.
- One shot = one primary beat. Two beats that need different framing are two shots.
- `used_s` is what the edit keeps; `gen_s` is what you generate (step 2 sets it).
- Every `avoid` item must carry its positive replacement (`avoid: red gloves -> both gloves are
  blue`). No Predis model exposes a negative-prompt field or a seed.
- Mark `audio: none` when sound is added in the edit. On Kling it cuts the price by a third.

## Step 2. Route each shot

Open [references/model-router.md](references/model-router.md). For each shot take the shot type,
the inputs it needs (first frame, last frame, identity refs, audio ref), `priority` and budget, and
pick default / cheap / premium. Then:

1. `list_models` once per session; confirm the pick is live.
2. `describe_model` once per picked model; write the exact option names and allowed values next
   to the shot. Every config key you send must come from this output.
3. Set `gen_s`: the model's smallest allowed duration that is >= `used_s` + 1.5 s (tail slack;
   last frames can break). Respect the model's min (Kling 3 Pro min 5, MiniMax min 5).

## Step 3. Compile

Open the model file from the table below and nothing else. Apply its **Compile** section to the
brief: slot order, length target, how timing is written, reference syntax, audio syntax, what to
drop because a reference already carries it, and the config mapping.

| Model ids | File |
|---|---|
| `veo_3_1`, `veo_3_1_fast` | [models/veo-3-1.md](references/models/veo-3-1.md) |
| `kling_3_pro`, `kling_3_standard` | [models/kling-3.md](references/models/kling-3.md) |
| `kling_o3_pro`, `kling_3_omni` | [models/kling-o3-omni.md](references/models/kling-o3-omni.md) |
| `kling_2_6`, `kling_2_5_turbo`, `kling_2_1` | [models/kling-2.md](references/models/kling-2.md) |
| `seedance_2_0`, `seedance_2_0_fast`, `seedance_2_5` | [models/seedance-2.md](references/models/seedance-2.md) |
| `seedance_1_5_pro`, `seedance_1_pro`, `seedance_1_lite` | [models/seedance-1.md](references/models/seedance-1.md) |
| `minimax_h3_max`, `minimax_hailuo_3` | [models/minimax-h3.md](references/models/minimax-h3.md) |
| `ltx_2_5_pro`, `ltx_2_5_fast`, `ltx_2_3_pro`, `ltx_2_3_fast` | [models/ltx.md](references/models/ltx.md) |
| `wan_2_7`, `wan_2_5_i2v`, `wan_2_2_i2v_fast` | [models/wan.md](references/models/wan.md) |
| `gemini_omni_flash` | [models/gemini-omni-flash.md](references/models/gemini-omni-flash.md) |
| `vidu_q3` | [models/vidu-q3.md](references/models/vidu-q3.md) |
| `grok_imagine_video_1_5`, `grok_video_extension` | [models/grok-video.md](references/models/grok-video.md) |
| `flux_3` (video) | [models/flux-3-video.md](references/models/flux-3-video.md) |
| `runway_aleph_2`, `wan_2_7_videoedit`, `dreamactor_m2` | [models/video-edit.md](references/models/video-edit.md) |
| `nano_banana_pro`, `nano_banana_2`, `nano_banana_2_1` | [models/nano-banana.md](references/models/nano-banana.md) |
| `gpt_image_2`, `gpt_image_2_5_sunburst`, `gpt_image_2_5_flare` | [models/gpt-image.md](references/models/gpt-image.md) |
| `seedream_5_pro`, `seedream_4_5`, `seedream_5_lite` | [models/seedream.md](references/models/seedream.md) |
| `flux_2_*`, `flux_1_*`, `flux_3_image` | [models/flux-image.md](references/models/flux-image.md) |
| `ideogram_v3_quality`, `ideogram_4_5`, `ideogram_4_5_precise_edit` | [models/ideogram.md](references/models/ideogram.md) |
| `recraft_v3` | [models/recraft.md](references/models/recraft.md) |
| `qwen_image_3`, `mai_image_2_5`, `grok_imagine_image_2`, `krea_2_turbo`, `p_image` | [models/image-others.md](references/models/image-others.md) |

Deeper field notes live in `predis-core:predis-prompting` (its references). Read them only when a
model file points there or a take fails twice.

## Look and style blocks

For any named look (light direction, Kelvin color temperature, aperture and focus, shutter / slow motion / motion blur, film stock, haze / dust / embers / backlit rain, skin and eye realism, character or prop reference sheets), load the matching file from the `prompt-styles` skill router and paste its block into the SET / LIGHT / MOTION / FILM / LOOK slot. Fill the brief's light, lens, motion and look fields with these blocks before compiling. Keep the model-specific syntax from the model file; take the look wording from prompt-styles. Same style line word for word in every shot. If `prompt-styles` is not installed, skip this step.

## Step 4. Self-check before any credit (mandatory)

For every compiled prompt, run the critique below, then the model file's own **Self-check**
list. Write the result into SHOTS.md as `check: PASS` or the failed items plus the fix. Rewrite
and re-check; max 2 rounds. A prompt that still fails is flagged to the user, not sent.

1. **Brief coverage:** subject (trait line verbatim), the one primary beat with an endpoint,
   camera (one move with start and end, or "static"), light source, look line. Missing = fail.
2. **Dialect:** the prompt follows the model file's slot order, length band and timing syntax.
   Count words; out of band = fail.
3. **References:** `reference_ids` order equals the numbering in the prompt; every reference has
   one stated role; the ref mode you picked exists in `describe_model`; a first-frame shot does
   not re-describe the frame.
4. **Contradictions:** the prompt does not ask for something the first or last frame already
   contradicts (for example "lifts him onto his shoulder" when the first frame already has him on
   the shoulder). Camera move and "static" never both appear.
5. **Avoid list:** every avoid item became a positive statement or a tolerated constraint line;
   no booster words (stunning, epic, masterpiece, 8K, cinematic as a lone adjective).
6. **Known failure modes:** read the model file's Failure modes table; if the shot hits one,
   apply the listed fix or re-route.
7. **Config:** every key and value is in `describe_model`; `audio` matches the brief; aspect and
   `gen_s` are allowed values; no locked option is overridden (Veo references mode locks 8 s).

## Step 5. Price, then hand off

- `estimate_cost` for every shot with its exact config (and `reference_ids` once they exist). Put
  the number next to the shot. Sum the job, add the retake budget for `priority: hero` shots
  (2 extra takes each).
- Over 150 credits total: show the user the shot table (shot, model, why, credits) and the total,
  and wait for a yes. Under 150: say the total in one line and go.
- Hand off to `predis-core:predis-generate` Step 5 (references) and Step 6 (run). It uses SHOTS.md
  as the source of every prompt and config. Do not rewrite prompts during the run loop; if a take
  fails, come back here, change one brief field, recompile, re-check.

## Rules

- Discover, never recall: model ids, option names and prices come from the live tools.
- One model per shot on purpose. Do not fire the same shot at two models hoping one lands; if
  unsure, draft on the router's cheap column first, then promote the winning prompt.
- Variety comes from changing the prompt, not the key: no seed is exposed.
- Talk to the user like a director: what each shot is for, which model and why in a few words, the
  price. No tool names or ids unless asked.
