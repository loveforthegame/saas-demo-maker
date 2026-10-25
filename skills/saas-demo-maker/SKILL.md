---
name: saas-demo-maker
description: >
  Makes short, story-led product ads (8 / 15 / 20 s, any aspect) for ANY SaaS or app: a named customer-hero in a
  vivid world, a spoken hook, the product's real loop as designed motion graphics, and a callback payoff. Asks
  for the product context first, pitches 3 concepts, shows a storyboard table for sign-off, then generates
  stills and video through the Predis MCP (Seedance 2.5) and builds and renders in HyperFrames. Use when: "make
  a demo ad / product ad / launch short / promo for <product>", "8 second ad for my app", "SaaS demo video".
  NOT for: long explainers or tutorials, screen recordings, or editing existing footage only.
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
| Prompts | `predis-director` (brief → model → dialect → self-check → price) + `prompt-styles` (light, film, motion, realism blocks). Bundled |
| Generation | Predis MCP connector: `add_reference`, `estimate_cost`, `generate`, `wait_for_run` |
| Build + render | `hyperframes`, `hyperframes-core`, `hyperframes-animation`, `hyperframes-cli` |
| On-screen copy | `ux-writing` if installed (grammar, claims, CTA) |
| New references | `watch` if the user brings new reference films to add to the borrow menu |

References in this skill: `references/borrow-menu.md` (hook/world/story/impact/motion/camera IDs),
`references/motion-recipes.md` (GSAP rebuild of every motion ID), `references/build-kit.md` (layout, helpers,
patterns that passed review, checks, gotchas).

## Step 1. Intake (ask once, then wait)

If the user gave a URL, read it first and pre-fill. Then ask only what is still missing, in one message:

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

Each concept must differ from earlier ads in hero, business, look and payoff shape. Wait for a pick.

## Step 3. Storyboard table in chat (gate 2 → spend)

Show the table **in the chat** and wait for an explicit yes on that table. A "go ahead" given before the table
was seen is not sign-off. Above it: story overview, the spoken lines, edit grammar, the one motif, impact budget.

| # | Time | Beat | Camera (one line) | Impact Y/N | Style | Borrowed from (IDs) | Credits |
|---|---|---|---|---|---|---|---|

Below it: credits total + ceiling (one re-shoot), and the rules checked.

**Length budgets** (from real builds; confirm each cap at intake):

| Slot | Shape | Impacts / motifs | Live clips | Credits (one round) |
|---|---|---|---|---|
| 8 s (≤9) | world shot with voice J-cut → hook-as-problem → spoken line → ONE product station (make step + ~1 s output tail) → callback → lockup 1.2 s | 1 / 1 | 3 × 5 s | ~330 |
| 15 s (≤16) | + a spot/insight beat, + optional integration beat (1–2 s) | 1–2 / 1–2 | 4–5 | ~450–550 |
| 20 s | 3 loops of the core cycle, longer output beat (~4 s), world proof | 2 / 2 | 5–6 | ~700–800 |

## Step 4. Generate (Predis MCP via predis-director + prompt-styles)

1. **Cast bible** in `SHOTS.md`, written once and pasted word for word: a trait line per character (and pet/prop),
   SET, LIGHT (Kelvin + source + what's not there), FILM (one stock, different from earlier ads), REALISM, MOTION.
2. **Stills, in parallel batches** (connector cap: 30 generations/hour):
   - character sheet(s): `nano_banana_pro`, 16:9, 2K, 3 panels on grey (~7 cr)
   - logo that says what the business is: `gpt_image_2_5_flare` 1024², text quoted and spelled letter by letter (~4 cr)
   - empty set plate(s): `nano_banana_pro` (~7 cr)
   - opening world shot with the logo on the sign: `gpt_image_2_5_flare` 1920×1080, logo as reference (~4 cr)
   - first frames: `nano_banana_pro` with refs (sheet, set), `outputs: 2` to pick from (~15 cr)
   - the product's outputs and any reference content shown in the UI (e.g. competitor posts): fictional, no real brands
3. **Check every still at full size** (identity, spelling, hands, the angle you planned) before animating.
4. **Video:** `seedance_2_5`, **720p**, `ref_mode: keyframes`, first frame only, `aspect: adaptive`, `audio: true`,
   5 s (94 cr) or 4 s (75 cr). Put spoken lines in quotes; write slow motion as a generated ramp, never a
   stretch. Fire all clips in parallel. `estimate_cost` first and state the price.
5. **QA:** timestamped frame grids, `whisper` for every spoken line, `predis:quality-gate` if installed.
   A weak shot is fixed in the edit first (punch-in, motif overlay, speed); re-shoot only if the edit can't.

## Step 5. Build in HyperFrames

Follow `references/build-kit.md`. Cut the live shots with intent (rules below), build product beats as
free-floating cards on a brand canvas, cite every motion device by ID. `lint` → `snapshot --at` every beat and
hand-off → fix → `render -f 60`. Then check duration ≤ cap and loudness.

## Step 6. Present, then log

Give the render path, the **as-built** beat table (time, beat, borrowed IDs), credits used this round and in
total, and any compromise you made (e.g. "the shake was weak, sold in the edit"). Say the 1080p render is
upscaled from 720p.

After every round, append the user's feedback to the project `NOTES.md`. If a note is a general rule, add it to
**Rules** below (one line, with the round it came from) instead of anywhere else. If the user says "no redoing
the videos", keep every clip and fix only the edit.

## Rules (each was a real rejection)

**Story**
- The hero is a customer of the product with a name, a business or role, and visual edge. Open on their world:
  the sign/logo and what they sell, and put "Name · Role, Business" on screen.
- The hero **speaks on camera** (1–2 short lines, lip-synced). No voiceover. Text never carries the story alone.
- A micro-arc even at 8 s: want → obstacle → turn (the product) → win, ending on a **callback** to the hook. Add
  one humour beat.
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
- Every prompt goes through `predis-director` + `prompt-styles`. Video on Seedance 2.5 at 720p unless the user
  says otherwise. Price before spending.
- Never reuse a previous ad's look, hero, business, music track or payoff shape.
