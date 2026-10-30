---
name: saas-demo-maker
description: >
  The entry point for short product videos for ANY SaaS or app, in two modes. Ad mode: story-led ads (8 / 15 /
  20 s, any aspect) with a named customer-hero, a spoken hook, the product's real loop as designed motion
  graphics and a callback payoff. Feature-hero mode: a silent, looping 12-20 s video that sits on a product or
  feature page and makes the viewer click the setup button. Asks for the product context first, pitches 3
  concepts, shows a storyboard table for sign-off, writes every prompt through the bundled prompting-guide into
  SHOTS.md, then generates through the Predis MCP and builds and renders in HyperFrames (HyperFrames is only the
  build step, never the entry point). Use when: "make a demo ad / product ad / launch short / promo for
  <product>", "8 second ad for my app", "SaaS demo video", "hero video for this page", "feature video",
  "in-app / onboarding video", "explainer loop for a feature". NOT for: long tutorials, screen recordings, or
  editing existing footage only.
---

# SaaS demo maker

A short product ad that works is a **tiny film about a customer**, not a feature tour. Every rule below came
from a real rejection while making three ads (20 s, 15 s, 8 s). The product is whatever the user brings; Predis
is only the generation engine (its MCP connector runs the image and video models).

**Three gates. No credit is spent before gate 3** (only free calls: `get_account`, `list_models`,
`describe_model`, `estimate_cost`).

## Skills this uses

| Step | Skill / tool |
|---|---|
| Prompts | `prompting-guide` (brief → route → compile → look blocks incl. realism → self-check → price). Bundled; a user-installed `prompting-guide` takes precedence |
| Generation | Predis MCP connector: `add_reference`, `estimate_cost`, `generate`, `wait_for_run` |
| Build + render | `hyperframes`, `hyperframes-core`, `hyperframes-animation`, `hyperframes-cli` |
| On-screen copy | `ux-writing` if installed (grammar, claims, CTA) |
| New references | `watch` if the user brings new reference films to add to the borrow menu |

References in this skill: `references/borrow-menu.md` (hook/world/story/impact/motion/camera IDs),
`references/motion-recipes.md` (GSAP rebuild of every motion ID), `references/build-kit.md` (layout, helpers,
patterns that passed review, checks, gotchas).

## Modes

| | Ad mode | Feature-hero mode |
|---|---|---|
| Where it plays | Feeds, ads, launch posts | A product or feature page, often a small player (~700-800 px wide) next to a setup button |
| Viewer | A stranger scrolling | A user who is already in the product and deciding whether to set the feature up |
| Job | Stop the scroll, make them want the product | Show the outcome in ≤2 s and make the setup feel like one step |
| Sound | Asked at intake | Silent. Text carries it; captions only on setup beats |
| Hero | A named customer who speaks on camera | The viewer's own kind of business. No single hero brand, no spoken lines |
| Length / end | 8 / 15 / 20 s, logo + CTA + URL lockup | 12-20 s, seamless loop, lockup = feature name (no URL; they are already in the app) |
| UI scale | As the format needs | 2-3× normal, at most 3-4 UI elements on screen; nothing that needs reading below ~14 px at player size |

Everything else (gates, story spine, prompting, generation, QA) is the same in both modes. A feature hero still
needs a story: hook event → the pain the feature removes → setup in one move → outcome in the viewer's world →
loop. "Simple" means fewer elements, never no story.

## Step 1. Intake (ask once, then wait)

If the user gave a URL, read it first and pre-fill. Then ask only what is still missing, in one message:

0. **Mode and placement:** ad or feature hero; where it plays and the player size; sound (silent / voice /
   music); the one action the viewer should take after watching.
1. **Product:** name, one-line what it does, who buys it (the customer the hero will be).
2. **Core loop:** the features in the order a user meets them. Which one is the **must-show "make/do" step**,
   which are short tails (e.g. publishing, sharing, syncing), and which are **out**.
3. **Integrations** to show (e.g. "works inside Claude/ChatGPT via MCP") and exactly what each can and cannot do.
4. **Facts allowed on screen:** verified numbers, feature names, trial terms, the CTA line and URL.
5. **Brand:** logo files (mark + wordmark), colours, font. Any past ads whose hero, business, look or ending
   must not be reused.
6. **Format:** aspect, which lengths, and the **hard max per length** (e.g. "8 s = ≤8.0 or ≤9.0?").
7. **Budget** in credits. Then run `get_account` to confirm the connector can generate and the balance.

Save answers to `BRIEF.md`. Do not assume a feature is wanted or excluded: ask.

## Step 2. Pitch 3 concepts (gate 1)

One line each, recommendation first. Each concept names:
- **Hero:** a named customer with visual edge and a 3-word tone ("Soggy. Proud. Deadpan."). Never a dull default.
- **World + business:** what they sell or do, and how the opening shot shows it (sign/logo + what it sells).
- **Signature action = product action:** the hero's physical move becomes the product beat (a dog's shake =
  the burst of outputs, a punch = the click, a wipe = the reveal).
- **Hook-as-problem** (an event in ≤2 s) and the **callback payoff** (same place or action, flipped).

Before pitching, name 3 overused ideas in this product category's ads; no concept may use them.

Before pitching, **watch every reference film the user points at, all of them, not a sample** (`watch`, or
local frame grids), and pull devices from `references/borrow-menu.md` by ID. Watching 3 of 10 references was a
real rejection.
Each concept must differ from earlier ads in hero, business, look and payoff shape. Wait for a pick.

## Step 3. Storyboard table in chat (gate 2 → spend)

Show the table **in the chat** and wait for an explicit yes on that table. A "go ahead" given before the table
was seen is not sign-off. Above it: story overview mapped to the five parts (see Story rules), the spoken lines, edit grammar, the one motif, impact budget.

| # | Time | Beat | Camera (one line) | Impact Y/N | Style | Borrowed from (IDs) | Credits |
|---|---|---|---|---|---|---|---|

Below it: credits total + ceiling (one re-shoot), and the rules checked.

**Length budgets** (from real builds; confirm each cap at intake):

| Slot | Shape | Impacts / motifs | Live clips | Credits (one round) |
|---|---|---|---|---|
| 8 s (≤9) | world shot with voice J-cut → hook-as-problem → spoken line → ONE product station (make step + ~1 s output tail) → callback → lockup 1.2 s | 1 / 1 | 3 × 5 s | ~330 |
| 15 s (≤16) | + a spot/insight beat, + optional integration beat (1–2 s) | 1–2 / 1–2 | 4–5 | ~450–550 |
| 20 s | 3 loops of the core cycle, longer output beat (~4 s), world proof | 2 / 2 | 5–6 | ~700–800 |

## Step 4. Generate (Predis MCP via prompting-guide)

**Gate 3: no `generate` call until the prompt is in `SHOTS.md` with a `check: PASS` line.** Invoke
`prompting-guide` and run its full pipeline (brief → route → compile → look blocks → Step 5 self-check) for every
shot, including "quick" stills and people who only appear for a second. Write each compiled prompt into
`SHOTS.md` exactly as it will be sent, followed by its check line. If a user picks a model or resolution the
router ranks lower (e.g. a non-default image model for faces), say so and give the trade-off before spending.

1. **Cast bible** in `SHOTS.md`, written once and pasted word for word: a trait line per character (and pet/prop),
   SET, LIGHT (Kelvin + source + what's not there), FILM (one stock, different from earlier ads), REALISM, MOTION.
   - Every shot with a realistic face gets the **full realism block** from `prompting-guide`
     (`references/styles/realism.md`), word for word, in both the still and the video prompt.
   - No boosters ("cinematic", "smooth", "8k"), no haze or dust unless the shot is about them, no golden-hour
     backlight by default. Ordinary light with a reason (window, overhead, practical lamp) and mid-task, unposed
     expressions read as real; stock-photo styling reads as AI.
2. **Stills, in parallel batches** (connector cap: 30 generations/hour):
   - character sheet(s): `nano_banana_pro`, 16:9, 2K, 3 panels on grey (~7 cr), after a casting pass of a few
     face options picked by taste
   - logo that says what the business is: `gpt_image_2_5_flare` 1024², text quoted and spelled letter by letter (~4 cr)
   - empty set plate(s): `nano_banana_pro` (~7 cr), lived-in (bags, notes, clutter of the trade)
   - opening world shot with the logo on the sign: `gpt_image_2_5_flare` 1920×1080, logo as reference (~4 cr)
   - first frames: `nano_banana_pro` with refs (sheet, set), `outputs: 2` to pick from (~15 cr)
   - the product's outputs and any reference content shown in the UI (e.g. competitor posts): fictional, no real brands
3. **Check every still at full size** (identity, spelling, hands, the angle you planned) before animating.
4. **Video:** `seedance_2_5`, **1080p for every clip that goes in the final cut** (720p only for draft passes;
   720p upscaled reads soft and waxes skin), `ref_mode: keyframes`, first frame only, `aspect: adaptive`,
   `audio` per intake (false for silent videos). Use the first ~2-3 s of each clip for close-ups; faces soften
   later in a clip. No extra scale push-ins on footage that is already upscaled. Put spoken lines in quotes; write slow motion as a generated ramp, never a
   stretch. Fire all clips in parallel. `estimate_cost` first and state the price.
5. **QA:** timestamped frame grids, `whisper` for every spoken line, `predis:quality-gate` if installed.
   A weak shot is fixed in the edit first (punch-in, motif overlay, speed); re-shoot only if the edit can't.

## Step 5. Build in HyperFrames

Follow `references/build-kit.md`. Cut the live shots with intent (rules below), build product beats as
free-floating cards on a brand canvas, cite every motion device by ID. `lint` → `snapshot --at` every beat and
hand-off → fix → `render -f 60`. Then check duration ≤ cap and loudness.

HyperFrames is the build step only. If `hyperframes init` writes a `CLAUDE.md` / `AGENTS.md` into the project
(its boilerplate says "start at /hyperframes"), delete them so later sessions route back through this skill.

## Step 6. Present, then log

Give the render path, the **as-built** beat table (time, beat, borrowed IDs), credits used this round and in
total, and any compromise you made (e.g. "the shake was weak, sold in the edit"). If any clip in the cut is
720p, say the render is upscaled from it.

After every round, append the user's feedback to the project `NOTES.md`. If a note is a general rule, add it to
**Rules** below (one line, with the round it came from) instead of anywhere else. If the user says "no redoing
the videos", keep every clip and fix only the edit.

## Rules (each was a real rejection)

**Story**
- The hero is a customer of the product with a name, a business or role, and visual edge. Open on their world:
  the sign/logo and what they sell, and put "Name · Role, Business" on screen.
- Ad mode: the hero **speaks on camera** (1–2 short lines, lip-synced). No voiceover. Text never carries the
  story alone. Feature-hero mode is silent: the outcome on screen carries it, with captions only on setup beats.
- A micro-arc even at 8 s: situation → desire → conflict → change (the product) → reward, ending on a
  **callback** to the hook. The conflict carries the story. Add one humour beat.
- The change is the loudest, least expected moment: the product breaks into the hero's world (not a quiet cut
  to a screen). Spend the impact there, with a grade flip (W10, recipe 7.14).
- Show the loop the product is built for, in the order users meet it. The core **make/do step is required at
  every length**. Output steps (publish, share, sync) can shrink to a ~1 s tail. Cutting an integration beat
  never cuts the core step.
- Integration beats (e.g. the product inside an AI chat) only claim what the integration can do, and visibly
  happen inside that host: the chat, the tool call, the results in the chat.

**Camera and edit**
- Camera grammar comes from the hero's world (skate: fisheye low follow, whips; pets: dog-eye level, slow-mo
  shake; DJ: platter top-down). Every live shot has a named, motivated angle (POV, subject-eye level, macro,
  OTS, crane, rack). No neutral wides.
- Hook in 1–2 s: an event, not a title.
- Cut on action and sound: J-cut the first line over the world shot, cut on the impact peak, use 0.3–1 s of
  silence as an impact.
- Live → UI goes through an object in the shot (zoom into the phone/screen); UI → live returns through a
  bubble or object.
- Not rushed: fewer micro-events, not faster cuts. Hold outputs ≥0.4 s, lockup ≥1.2 s. At 8 s, one UI station.
- The length cap is hard. Cut beats or holds; never overrun.

**Motion graphics**
- No fake app chrome (sidebars, nav, settings rows, page swaps). Product beats are designed, free-floating cards on a
  brand canvas that echoes the hero's world. Real-looking third-party UI (social posts, platform icons) only
  where the story needs it, never cropped.
- Borrow every device from the borrow menu by ID and cite it. One-take virtual camera, depth, one easing family,
  curved cursor paths, press springs. No particle confetti, random pops, shake or flash filler.
- One world motif carried across every cut (e.g. water droplets become the outputs, then fall to destinations).
- Impact budget per the length table; spend it on the hook, the product turning on, or the payoff.

**Copy and claims**
- Proper grammar and capitalisation. Prompts on screen sound like the hero (3–8 words).
- Only facts from the intake. No invented numbers. Lockup = logo + one line + CTA with URL.

**Generation**
- Every prompt goes through `prompting-guide` and sits in `SHOTS.md` with a PASS line before it is sent (gate 3).
  Video on Seedance 2.5, final clips at 1080p. Price before spending.
- Never reuse a previous ad's look, hero, business, music track or payoff shape.

## Failure log: feature ad, 3 rounds, ~1,900 credits for one approved 18 s ad (2026-10-27)

Round 1 (~620 cr) rejected: "video, audio, camera angles all bad, rushed". Round 2 (~660 cr) rejected: "a product demo, no hook, no story, the skills weren't used, background too strong, slow". Round 3 approved as "okay". Each rejection repeated a rule already written here, so most of the spend was avoidable.
- **Pick the business for instant recognition first, edge second.** A niche trade (neon-sign maker) needed explaining. An everyday shop with a daily-output reason to post (gelato, a new flavour each day) read in under a second.
- **Ask about sound at intake.** The user wanted a silent, text-led promo. A voice, music and SFX mix that was never asked for cost a full round.
- **Generate live shots at 1080p.** 720p upscaled reads as "bad quality". Camera: close, eye level, slow push-ins. Crane wides, fisheye and whips read as cheap.
- **A feature walkthrough is not an ad.** Keep the metaphor and story spine (hook event, problem, turn, product, payoff, callback) even when the user asks for a "simple" promo. Simple means fewer elements, never no story. One visual metaphor carries it, for example "unposted content melts; the product rewinds the melt; the shop's display case is the calendar".
- **Beats of 1.5–2.5 s.** 3 s per beat felt slow. Keep footage bright; don't bury it under dark overlays. Product beats go on a designed canvas, not busy photos dimmed behind cards.
- **Render QA, not only snapshots:**
  - `data-playback-rate` can be ignored at render, so bake speed changes and reverses into the file with ffmpeg.
  - A font family named "Serif" collides with the generic serif and silently falls back, so give fonts unique names.
  - Run `freezedetect` (d=1.0) and add a drift to any hold.
- **Don't spend until the story is signed off.** Show the metaphor and the storyboard table before any generation, every round, including when the user says "just make it".

## Failure log: feature hero, 1 round, 315 credits, fully rejected (2026-10-30)

A silent in-app hero for an auto-publishing feature. Verdict: "the characters look AI, the motion graphics are bad, the videos are bad, not enticing at all."
- **The prompting pipeline was skipped.** Prompts were hand-written with no character sheets, no realism block, a "cinematic film still" opener, golden-hour backlight and dust haze in every shot, and posed, smiling model faces. The faces came out waxy. Earlier films that ran the full pipeline had faces that passed. Gate 3 exists because of this.
- **The user's model and resolution picks were followed without flagging the trade-off.** A weaker image model for faces plus 720p video, upscaled and pushed in, made the faces softer at every stage.
- **The feature hero tried to show everything:** 3 example businesses, 3 input sources, 3 platforms and a 28-cell month grid in 18 s. At a ~770 px player nothing could be read and nothing landed. Show one idea per beat, with 3-4 large UI elements at most.
- **Only 3 of 10 reference films were watched** before planning.
