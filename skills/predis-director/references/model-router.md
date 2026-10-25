# Model router

Prices: `estimate_cost` on 2026-10-15, 9:16, default resolution unless noted. They move; re-price
every job. Full option catalog: `predis-generate/references/models.md`.

## How to pick (in this order)

1. **Hard inputs first.** What must the model accept? First frame, last frame, N identity refs,
   a video ref, an audio ref, native audio, a duration under 3 s or over 10 s. Drop every model
   that cannot (table "Input map" below).
2. **Shot type** -> the row in the router table.
3. **Priority + budget** -> column. `hero` = default or premium; `support` = default; `filler` and
   drafts = cheap.
4. **Sound plan.** If sound is added in the edit, prefer models where audio off is cheaper
   (Kling 3 family) and set audio off. If the shot needs lip-sync, only native-audio models or an
   audio-ref model qualify.
5. Write one line per shot: `S6 -> kling_3_pro (fast-action, hero, physics) 91 cr`.

## Router table: images (credits per image)

| Shot type | Default | Cheap | Premium | Why |
|---|---|---|---|---|
| hero-still / keyframe (photoreal) | `nano_banana_pro` 7 | `nano_banana_2_1` 2 | `gpt_image_2_5_sunburst` q=high 4 | Nano Banana reasons over natural language and holds up to 14 refs |
| character-sheet / consistent cast stills | `nano_banana_pro` + refs 7 | `seedream_4_5` + refs 3 | `gpt_image_2_5_flare` + refs 4 | multi-ref identity; Seedream is good at turnarounds |
| text-graphic (poster, thumbnail, UI, ad copy) | `gpt_image_2_5_flare` q=high 4 | `ideogram_4_5` 5 | `ideogram_v3_quality` 7 (logos, typography) | GPT Image renders quoted text verbatim; Ideogram for type-led design |
| fix text in an existing image | `ideogram_4_5_precise_edit` 5 | `gpt_image_2` edit 4 | | source slot + local edit |
| vector-flat / icon / brand mark | `recraft_v3` style=digital_illustration 3 | `flux_2_pro` 2 | | Recraft style enum sets the medium |
| product-still | `nano_banana_pro` + product ref 7 | `flux_2_pro` + hex 2 | `flux_2_max` 6 | FLUX holds hex colours tied to objects |
| draft-still (composition, moodboard) | `flux_1_schnell` 0.24 | `p_image` 0.41 | `krea_2_turbo` 0.64 | near free, no text, no refs |
| stylized / bold | `grok_imagine_image_2` 5 | `seedream_5_lite` 3 | `seedream_5_pro` 5 | |

## Router table: video (credits at the stated duration)

| Shot type | Default | Cheap | Premium | Why |
|---|---|---|---|---|
| character-performance (face/body beat, no lines) | `minimax_h3_max` 5 s 33 | `seedance_1_5_pro` 5 s 11 | `kling_o3_pro` + identity refs 5 s 46 | H3 is fast (~35 s) and strong on one-beat acting; cheap retakes |
| dialogue-lipsync (native voice) | `veo_3_1` 8 s 169 (4 s 85) | `veo_3_1_fast` 8 s 51 | `kling_3_pro` audio on 5 s 137 | Veo does dialogue + SFX + ambience in one pass |
| lipsync to a voice file you have | `wan_2_5_i2v` + audio ref 5 s 41 | `seedance_2_0` + audio ref | `dreamactor_m2` (driving video) 4 cr/s | audio slot drives mouth and rhythm |
| fast-action / physics / stunts | `kling_3_pro` audio off 5 s 91 | `kling_2_5_turbo` 5 s 28 | `seedance_2_5` 8 s 150 | Kling 3 is the most reliable with bodies, weight and contact |
| identity-locked-motion (same face across shots) | `kling_o3_pro` first frame + 4 refs, 5 s 46 (4 s 36, 3 s 27) | `seedance_2_0_fast` refs 5 s 49 | `kling_3_omni` 7 refs, 5 s 68 | first frame AND identity refs in one call |
| crowd / ensemble energy | `seedance_2_0` 720p 4 s 49 | `seedance_2_0_fast` 5 s 49 | `seedance_2_5` 8 s 150 | many bodies moving coherently |
| multi-shot-sequence in one clip | `seedance_2_0` 10-15 s, 12 cr/s | `seedance_2_0_fast` 10 cr/s | `seedance_2_5` up to 30 s + audio, 19 cr/s | labelled shots honoured; `kling_3_pro` also cuts on labels |
| product-motion / controlled arc (A to B) | `kling_3_standard` first+last, audio off 5 s 68 | `ltx_2_3_pro` first+last 6 s 29 | `veo_3_1` keyframes 8 s 169 | last-frame slot locks the end state |
| macro-texture / liquids / light | `veo_3_1` 4 s 85 | `ltx_2_3_fast` 3 cr/s | `ltx_2_5_pro` 8 s 111 | |
| establishing / environment | `veo_3_1_fast` 8 s 51 | `wan_2_7` 5 s 61 | `flux_3` (21:9 to 9:16, up to 20 s) 14 cr/s | |
| stylized-anime | `grok_imagine_video_1_5` 6 s 68 | `seedance_1_5_pro` 11 | `seedance_2_0` + style ref | |
| short-insert (edit keeps < 2 s) | `grok_imagine_video_1_5` 3 s 34 (1 s steps) | `seedance_1_pro` 2 s min, 4 cr/s | `kling_o3_pro` 3 s 27 | do not pay for 5 s you will cut |
| long-take (> 10 s, one shot) | `ltx_2_3_fast` up to 20 s, 3 cr/s | `wan_2_7` up to 15 s | `seedance_2_5` up to 30 s | |
| motion draft before a hero run | `wan_2_2_i2v_fast` 5 s 9 | `seedance_1_5_pro` 5 s 11 | `kling_2_5_turbo` 5 s 28 | test motion and blocking, then promote the prompt |
| restyle an existing clip | `runway_aleph_2` 27 cr/s | `wan_2_7_videoedit` 8 cr/s | `kling_3_omni` + refs | |
| extend a clip | `grok_video_extension` 4 cr/s | `gemini_omni_flash` 5 cr/s | | |
| motion-transfer | `dreamactor_m2` 4 cr/s | `seedance_2_0` video ref | | |
| all-rounder, cheapest acceptable | `gemini_omni_flash` 5 cr/s (picks own length) | | | |

## Input map (from describe_model, 2026-10-15)

| Need | Models that accept it |
|---|---|
| first + last frame | veo_3_1(+fast), kling_3_pro, kling_3_standard, kling_2_1, seedance_2_0(+fast), seedance_2_5, seedance_1_5_pro, seedance_1_pro, minimax_hailuo_3, minimax_h3_max, wan_2_7, ltx (all 4), flux_3, vidu_q3 |
| first frame only | kling_2_6, kling_2_5_turbo, seedance_1_lite, wan_2_2_i2v_fast, wan_2_5_i2v, grok_imagine_video_1_5, kling_o3_pro |
| first frame + identity refs in one call | kling_o3_pro (1 + 4) |
| identity/style refs (no first frame) | veo (3, locks 8 s), seedance_2_0 (9), seedance_2_5 (30), kling_3_omni (7 + 1 video), minimax_hailuo_3 (9), gemini_omni_flash (10), vidu_q3 (4), grok_imagine_video_1_5 (7, locks 720p) |
| video ref | seedance_2_x, kling_3_omni, minimax_hailuo_3, gemini_omni_flash, runway_aleph_2, wan_2_7_videoedit, dreamactor_m2, grok_video_extension |
| audio ref | seedance_2_x, minimax_hailuo_3, wan_2_5_i2v |
| native audio switch | veo, kling_3_*, kling_o3_pro, kling_2_6, kling_3_omni, seedance_2_x, seedance_1_5_pro, ltx, flux_3, vidu_q3 |
| durations | veo 4/6/8; kling_3 5-10; kling_o3 3-15; kling_3_omni 3-15; seedance_2_0 4-15; seedance_2_5 4-30; seedance_1_pro/lite 2-12; minimax 5-15; wan_2_7 2-15; ltx fast 6-20; ltx pro 6-10; grok 1-15; vidu 4-8; flux_3 5-20 |
| aspect beyond 16:9/9:16/1:1 | seedance, minimax, wan_2_7, vidu, grok, flux_3 (21:9) |
| negative prompt or seed field | none (all models) |

## Price levers worth knowing

- Kling 3 Pro audio off 91 vs on 137 (5 s). Kling O3 Pro 46 vs 57. Seedance 2.0 audio does not
  change the price. Veo does not either.
- Seedance 2.0 1080p costs 2.5x 720p (152 vs 61 at 5 s). Draft at 720p.
- Duration is linear on most models: a 3 s Kling O3 shot is 27, not 46.
- Hero shots: budget 2 retakes. Performance and dialogue shots: 2 to 3 takes, keep the clean one.
