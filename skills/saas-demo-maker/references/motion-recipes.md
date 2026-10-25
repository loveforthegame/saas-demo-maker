# Motion recipes (cite by ID: "Creatify 7.9", "pool lady 7.6", "motion-ref T6")
GSAP rebuilds of every device in the borrow menu. Headings keep the original numbering so storyboard citations resolve.

## Creatify 7.x

### 7.1 Hyperspace-to-subject drop-in
- 0.9 s of radial streaks with growing length, then the subject appears small at the vanishing point and pops to full size in about 3 frames with an overshoot. The streaks cross-fade out in those same frames.
- **GSAP:** `tl.to(stars,{z:1,duration:.8,ease:"power3.in"}).fromTo(hero,{scale:.4,filter:"blur(10px)",opacity:0},{scale:1.05,filter:"blur(0px)",opacity:1,duration:.12,ease:"expo.out"}).to(hero,{scale:1,duration:.15,ease:"sine.out"}).to(hero,{rotation:3,x:8,duration:2.2,ease:"sine.inOut"})`

### 7.2 Logo split-reveal ("A becomes A MCP × B")
- The centred "creatify" (3.37–3.55) slides left by about 22 % of the frame width in 0.25 s with horizontal motion blur. "MCP" (bold italic, navy `#2A1C79`) wipes in to the right of the wordmark. The ChatGPT mark and wordmark slide in from the right **in grey at 50 % opacity, sitting about 6 px low**, then rise and darken to black while the "×" fades in (3.8–3.9). The whole group then drifts right/up about 10 px over the hold (a living hold, never frozen).
- At the end (20.1–20.5) the same lockup is **reversed in assembly**: the big ChatGPT mark shrinks into its slot while "creatify MCP" slides in from the left in grey and darkens.
- **GSAP:** `tl.to(logoA,{xPercent:-55,duration:.25,ease:"power3.inOut"}).from(mcp,{clipPath:"inset(0 100% 0 0)",duration:.2},"<.05").from(logoB,{x:120,opacity:.3,color:"#999",y:6,filter:"blur(6px)",duration:.3,ease:"power3.out"},"<").from(x,{opacity:0,scale:.5,duration:.15},"-=.1").to(group,{x:10,y:-4,duration:1,ease:"none"})` plus a CSS `filter: blur()` keyed to velocity (or a pre-baked directional blur via an SVG `feGaussianBlur stdDeviation="8 0"`).

### 7.3 Whip-pan scene change (vertical and horizontal)
- The outgoing element translates out by 100 % of the viewport in about 0.15 s while the incoming element arrives from the opposite edge. Both carry **directional blur** (about 20–30 px along the axis) only during the move. The incoming element overshoots in scale (1.2) and settles in 0.3 s.
- Used at 4.8 s (lockup goes up, card comes from below), 10.0 s (menu to composer, with a horizontal smear) and 17.4 s (side cards fly out left and right).
- **GSAP:** `tl.to(out,{yPercent:-120,filter:"blur(0 24px)",duration:.15,ease:"power2.in"}).fromTo(in,{yPercent:120,scale:1.2},{yPercent:0,duration:.18,ease:"power3.out"},"-=.05").to(in,{scale:1,duration:.3,ease:"back.out(1.4)"})`. In HTML, fake the axis blur with an SVG filter `stdDeviation="0 12"`, animated to 0.

### 7.4 Background luminance dip (focus spotlight)
- The canvas fades `#FAFAFA` → `#000` in 0.4 s (5.5–5.9) while the camera pushes in 1.6x on the card. The card stays white with a soft white glow (an outer shadow of about 40 px at `rgba(255,255,255,.15)`). It returns black → white in 0.4 s (7.1–7.5) right before the Add click.
- **GSAP:** `tl.to(bg,{backgroundColor:"#000",duration:.4,ease:"power2.inOut"}).to(cam,{scale:1.6,duration:.5,ease:"power3.out"},"<")` … `.to(bg,{backgroundColor:"#FAFAFA",duration:.4},"setupEnd-.4")`.

### 7.5 Synthetic typing with a caret
- "Creatify" (8 chars) takes about 0.4 s (about 20 chars/s). The URL "https://api.creatify.ai/mcp" (27 chars) takes about 0.55 s (about 50 chars/s). The long prompts run at about 25–35 chars/s. The caret `|` is visible during typing and stays after it. The text colour in the inputs is violet `#6A5AE0` (placeholder-like). The newest character fades in over about 2 frames (visible as a lighter last glyph at 10.3–10.7 s).
- Long prompts that overflow the frame **truck the camera with the caret** instead of wrapping.
- **GSAP:** use a TextPlugin, or step a `textContent` slice on an `onUpdate`, `ease:"none"`, with duration = chars / 30. Keep the caret blink off during typing and switch it on (0.5 s step) when idle.

### 7.6 Cursor choreography
- A large black macOS-style arrow (about 40 px at 1080p, with a white stroke and a soft shadow) moves on **curved, ease-in-out paths** of 0.25–0.4 s. Each click shows as the target scaling to 0.92 for about 3 frames and then a glow. The cursor moves first and the camera follows about 0.1 s later (a lag that makes the camera feel handheld or virtual).
- **GSAP:** `MotionPathPlugin` with a 2-point bezier, `duration:.35, ease:"power2.inOut"`. On click: `to(btn,{scale:.92,duration:.06}).to(btn,{scale:1,boxShadow:"0 0 0 6px rgba(92,78,243,.35),0 0 24px rgba(92,78,243,.5)",duration:.25,ease:"back.out(2)"})`, then fade the glow in 0.3 s.

### 7.7 Card-to-app morph (crash zoom into the UI)
- At 8.3–8.6 s the camera zooms *into* the card (scale about 2, blur) and on the next frame the ChatGPT app window appears small and blurred, already in the same spot, then pulls back sharp. It reads as "the card was inside the app".
- **Rebuild:** `tl.to(card,{scale:2.2,filter:"blur(8px)",duration:.15,ease:"power2.in"}).set(card,{opacity:0}).fromTo(app,{scale:.6,filter:"blur(10px)"},{scale:1,filter:"blur(0)",duration:.3,ease:"expo.out"})`, then `.to(cam,{scale:1.8,x:...,duration:.5,ease:"power3.inOut"})` to push to the composer.

### 7.8 Dropdown and highlight scrub
- A "+" tooltip ("Add files and ...", black pill) appears in 0.1 s on hover. The menu unfurls downward in about 0.2 s: the panel height grows and the rows fade in with a 30 ms stagger. A grey highlight bar (`#EDEDED`) **steps** row to row with the cursor, about 0.12 s per row (Add photos & files → Web search → Deep research → OpenAI Platform → Creatify MCP). Selecting puts a "Creatify MCP" chip (icon + blue `#3B82F6`-ish label) into the composer.
- **GSAP:** `from(rows,{opacity:0,y:-6,stagger:.03,duration:.15})`, and highlight `to(bar,{y:rowY,duration:.1,ease:"power2.out"})` per step.

### 7.9 Holographic "develop" reveal for AI results (the hero technique)
- The three ad cards appear **staggered left to right at about 0.1 s intervals** (12.6, 12.7, 12.8 s), starting as nearly white ghosts (opacity about 0.3). They show an **iridescent thermal/holographic colour map** (pink, cyan, lime, violet, a hue-rotated and posterised version of the image) that **resolves to true colour over about 0.9 s**, left card first. A slight upward drift of about 20 px. The composer pill slides up from the bottom at 13.1 s.
- The same effect runs at 16.0–16.8 on a *single* card to signal "this one is transforming" (still to video), plus a 2 px pink-violet glow border (`#E6A3D8` → `#B18CF0`).
- **Rebuild (HTML):** stack two copies of the image. The top copy has `filter: hue-rotate(0deg) saturate(3) contrast(1.4)` plus `mix-blend-mode: difference` over a conic gradient (`#ff9ad5,#7cf5ff,#c4ff7a,#b38cff`). Animate the overlay: `to(holo,{opacity:0,"--hue":180,duration:.9,ease:"power2.out",stagger:.1})`, card `from({opacity:.3,y:20,duration:.4,stagger:.1})`. A Canvas or WebGL alternative is a gradient-map shader with time-shifted hue.

### 7.10 Still-to-video expansion
- The chosen card starts to *move* inside its square crop (the couple starts drinking). The prompt pill drops down and blurs out (17.4 s). The neighbours slide out left and right with blur (0.15 s). The card animates its aspect ratio **1:1 → 16:9** and its scale about 1.8x in about 0.3 s (`power3.inOut`). The rounded corners (about 12 px) and soft shadow stay, so it is still "a UI object" while it plays real footage. Two internal hard cuts follow (18.08, 19.49).
- **GSAP:** use Flip (`Flip.getState(card)`, then change the class to `.wide`, then `Flip.from(state,{duration:.35,ease:"power3.inOut"})`) while the `<video>` inside does `object-fit:cover`.

### 7.11 Logo-rise wipe to end card
- The ChatGPT mark (black, thick stroke) enters from below frame (19.3 s) and scales from about 0.5 to 1.4 while rising to centre over 0.7 s. The video behind blurs (to about 20 px) and fades to 30 % opacity. The mark then shrinks (about 0.15 s) into the lockup slot (see 7.2).
- **GSAP:** `fromTo(mark,{yPercent:150,scale:.5},{yPercent:0,scale:1.4,duration:.7,ease:"power3.out"}).to(videoCard,{filter:"blur(20px)",opacity:.3,duration:.5},"<.2")`.

### 7.12 Typed URL with a gradient resolve
- The URL types in dark grey `#333` at about 50 chars/s (21.4–22.0). Then, over 0.3 s, the fill becomes a **horizontal gradient `#DE7B97` (pink) → `#9268CD` → `#5E4CD9` (violet)**. A 3 s hold, then black.
- **CSS:** `background:linear-gradient(90deg,#DE7B97,#5E4CD9);-webkit-background-clip:text;color:transparent`. Cross-fade from a solid-colour layer in 0.3 s.

---

## pool lady 7.x

### 7.1 Voice orb + two-line rolling caption (signature device)
- Purple-to-blue sphere (~110 px at 1276 wide) with a white sine-wave glyph and a soft outer glow (radius ~1.5x the sphere), placed in the left third over live footage. The caption is centred under it in white sans (~22 px), max 2 lines, about 3-4 words per line.
- **Caption roll:** line 1 appears at 100% opacity. When the next phrase starts, line 1 slides up ~20 px and drops to ~35% opacity (and slightly blurs) while line 2 fades in below at 100%. Example: 05.55 "I want to launch" (white) + "paid ads" (ghost) → 06.3 "I want to launch" (ghost) + "paid ads" (white). Karaoke by phrase, not by word.
- Orb in: scale 0.6→1 plus opacity, ~250 ms, back-out. The wave glyph keeps oscillating. Orb out: hard cut with the shot.
- **GSAP:** `tl.from(orb,{scale:.6,autoAlpha:0,duration:.25,ease:"back.out(2)"}).from(line1,{y:10,autoAlpha:0,duration:.2},"<.1").to(line1,{y:-18,opacity:.35,filter:"blur(1px)",duration:.3,ease:"power2.out"},"+=.7").from(line2,{y:12,autoAlpha:0,duration:.3,ease:"power2.out"},"<")`. Glow: `box-shadow:0 0 40px 12px rgba(110,80,255,.55)`. Sphere: `radial-gradient(circle at 35% 30%, #8F7BFF, #5531F0 55%, #3A1FC9)`.

### 7.2 Camera-pan prompt bar ("long input, short screen")
- A white pill input (radius = height/2, 1 px #ECECF0 border, soft shadow) on a #FAFAFC canvas, **scaled so it is ~2.5x wider than the screen**. The virtual camera starts on the left logo ("Higgsfield" lime icon plus blue word), types the `/command` in blue, then **whip-pans right** through the prompt text (heavy horizontal motion blur, 2-3 frames per whip, 2-3 whips), settles on "GPT-6 Astra ▾" and the blue round send button.
- Typing: ~25-30 chars/s, with the newest chars in blue (#2D8CFF) that turn black.
- Send: a **blue pixel-block shimmer** (8-12 px squares, blue/cyan, 60% opacity) flickers behind the model name for ~0.5 s. The send button gains a glow ring, then the camera pushes in ~10% and blurs out to the next card.
- **GSAP:** put the bar in a `.stage` and animate `x` of the stage: `to(stage,{x:-900,duration:.18,ease:"power4.inOut"})` with `filter:"blur(8px)"` peaking mid-tween (via a keyframe: blur 0→10→0). Typing with a TextPlugin-like steps tween. Pixel shimmer = a grid of divs with a random `opacity` stagger `{each:.03, from:"random", repeat:3, yoyo:true}`.

### 7.3 Blur-through z-push between UI cards
- Each form step (business → objective → budget → map → ad identity → preview → table) is a separate card on white. Transition: the outgoing card scales 1→1.15, blurs 0→12 px and fades, while the incoming card starts at scale 0.9, blur 10 px and fades in. ~300-400 ms total, overlapping. Card position alternates (left-aligned at 00:12 and 00:15, centred at 00:10 and 00:13, right at 00:14), so the eye zig-zags.
- Inside a card: field focus = a pale blue fill (#DCEBFB) with a blue glow on the active dropdown (00:11). The Continue button goes grey→blue (#3B82F6) once filled. Numbers type in ($0 → 719 → 1,000).
- **GSAP:** `tl.to(out,{scale:1.15,filter:"blur(12px)",autoAlpha:0,duration:.35,ease:"power2.in"}).fromTo(in,{scale:.9,filter:"blur(10px)",autoAlpha:0},{scale:1,filter:"blur(0)",autoAlpha:1,duration:.4,ease:"power3.out"},"-=.2")`.

### 7.4 3D curved wall of ad cards with tag pills
- ~20 vertical 9:16 reel thumbnails (real-looking UGC pool videos) on a curved/barrel surface, each with a small rotated-sticker tag pill (pink #E8337A, cyan #3EC7E8, lime #C6F432; tiny white text like "Sensory sound hook", "Reflection detail", "Human introduction"). The camera pushes forward and trucks right for ~4.5 s. Cards nearer the edges are larger and more blurred (lens distortion).
- **GSAP/CSS:** a container with `perspective:900px`; cards positioned on a cylinder (`rotateY(i*8deg) translateZ(-1200px)`). Animate the container `z` 0→400 and `rotateY` -6°→6° over 4.5 s with `ease:"none"`. Tags: `rotate(-6..6deg)`, entering with a 60 ms stagger `scale:0→1, ease:"back.out(3)"`.

### 7.5 Floating comment cards
- Reddit/IG-style comment cards (avatar dot, handle, 1-line comment, likes/reply row) scattered at 3 depths (small/soft back layer, sharp front layer), drifting up ~20 px/s. Exit: whole-layer whip-left with motion blur (00:34.0).
- **GSAP:** 3 layers with different `y` speeds (parallax), then `to(layers,{x:-1400,filter:"blur(14px)",duration:.3,ease:"power3.in",stagger:.03})`.

### 7.6 Clip-to-preview fly-in (UGC becomes an ad)
- The vertical clip enters from the lower-left (offset ~-250 px x, +120 px y), rotated ~-12°, with motion blur, into the empty "Your video preview" slot. It lands at a slight +6° tilt, then straightens to 0° and fills the Instagram Reels mock (handle @thepoolladyco, "Send message" CTA). A mouse cursor is visible "dropping" it (46.7). ~600 ms.
- **GSAP:** `fromTo(clip,{x:-260,y:140,rotation:-14,scale:.8,filter:"blur(6px)"},{x:0,y:0,rotation:6,scale:1,filter:"blur(0)",duration:.45,ease:"power3.out"}).to(clip,{rotation:0,duration:.25,ease:"back.out(2)"})`.

### 7.7 Ads Manager table reveal
- The table first appears blurred and smaller with 1 row (V01). After a push-in and de-blur, 5 rows (V01-V05) are present with blue toggles on and "• In review". Rows don't animate individually; the "more ads" change happens inside the blur. That is the cheap and effective way to multiply results.

### 7.8 Lime gradient wipe reveal of generated reels
- 3 vertical reels in a row. Each starts as a lime (#C6F432) to white vertical gradient block and wipes down/clears to the video, staggered L→R ~120 ms (00:53.0 shows card 1 revealed, card 2 mid-wipe, card 3 still lime). Each reel has bold all-caps hook text burned in near the bottom and IG UI chrome.
- **GSAP:** an overlay div per card with `background:linear-gradient(#C6F432,#fff0)`; `to(overlay,{yPercent:100,duration:.4,ease:"power2.inOut",stagger:.12})`.

### 7.9 In-world notification bubble ("CAMPAIGN UPDATE / 12 NEW LEADS")
- A speech-bubble pill (lime-to-olive gradient #B9DB6E→#7FAE3F, inner highlight, 1 px light stroke, downward pointer tail) placed **directly above the real phone on the table**, so it reads as coming from the phone. The label "CAMPAIGN UPDATE" sits above it in small white caps; the main text is condensed bold white caps.
- Timing: pops at 01:07.4 (scale 0→1 from the tail point, ~200 ms back-out). The background racks focus from her to the phone 01:07.6-01:08.0. Holds ~1.6 s, then **shrinks back into the phone** (01:09.0, scale →0 toward the tail, ~250 ms). Focus racks back to her; she smirks at 01:10.5.
- **GSAP:** `transformOrigin:"50% 100%"`; `from(bubble,{scale:0,duration:.22,ease:"back.out(2.5)"})`, label `from({y:6,autoAlpha:0},"<.08")`; fake the rack focus with two video layers or `filter:blur()` crossfade on the bg (0→6 px, 400 ms).

### 7.10 Title lens / astroid frame (hook)
- A glass orb that refracts the footage (displacement plus a blue tint) grows from 5% to 40% of frame width. Then two concave star-edge shapes slide in from the screen edges to frame the centred title.
- **HTML:** an SVG `feTurbulence`/`feDisplacementMap` lens, or a CSS `backdrop-filter:blur(2px) saturate(1.4)` circle with a radial blue gradient. Astroid = an SVG path with 4 concave arcs, filled with `linear-gradient(#2D8CFF, #A6D1FF)`, entering `x:±300→0, duration:.35, ease:"expo.out"`.

### 7.11 Live↔UI transitions
- World→UI: always a **hard cut** from letterboxed footage to the white canvas (the bars disappear: frame-shape change = world change).
- UI→world: hard cut as well, sometimes right after a push-in plus blur (00:18.2).
- Inside UI: only blur pushes and whip-pans, no hard cuts.

## adilitos 7.x

### 7.1 Word-stack hook text
3 lines left-aligned at mid-frame to the right of the hero ("I sell / *burritos* / now."). Each word appears in place with a fast opacity cut and a tiny upward settle, ~100 ms apart. The key noun is bold italic. Lime #D6F536, no stroke, slight glow.
GSAP: `tl.from(words,{opacity:0,y:8,duration:.12,ease:"power2.out",stagger:.1})`. Hold for the rest of the shot, then cut out with the shot.

### 7.2 STEP chapter label
"STEP 1" (bold, all caps, lime, ~44px at 720w) is typed in place ("STEP" at 11.9, "1" at 12.0). One beat later (~1 s) a white semibold sentence-case title writes on below it ("Help" → "Help people find me", word by word), placed left-mid over the scene. At STEP 2 the label enters big mid-frame (~80px) with a blurred-in title, then **shrinks and moves down** to a lower-centre block above the food (34.8→36.4, ~1.2 s, ease-in-out).
GSAP: label `from {opacity:0, scale:1.15, filter:"blur(6px)"} .25s power3.out`; title words `stagger .08`; for the STEP 2 variant `to(group,{scale:.6,y:+180,duration:1.2,ease:"power2.inOut"})`.

### 7.3 Spoken captions (two modes)
- Over live shots: small white sans (~22px at 720w), 1–3 words at a time, centred at ~70% height, soft drop shadow. They change every 300–500 ms in sync with speech.
- Over UI: the same captions turn **light blue #3AA6DC** on white and sit under the UI card, so they read as part of the UI page.
GSAP: swap text per word chunk with `opacity 0→1 .08s`; no movement.

### 7.4 Orb hand-off (live → UI). **Signature transition**
13.8: a small glowing blue sphere (~20px) appears over the laptop in the live shot and grows to ~70px by 14.1 (ease-out), then floats with the chef's hand (it is tracked to his hands, drifting ±10px). Caption "Hey chat" then "Set up / my paid ads with". At 15.2 the caption is replaced by a **Higgsfield logo + wordmark that types in letter by letter** (15.2–15.6). Hard cut at 16.1 to a white screen where the **same orb is now large (~260px), centred**, a cloud-textured blue gradient with an outer blur glow, "ChatGPT" label above, and the reply "Sure, I can help with that." revealed word by word under it (16.1–17.0, with the later words in grey fading to black).
GSAP: orb `radial-gradient(#fff 0, #7EA2FF 45%, #3D5BF5 80%)`, `box-shadow 0 0 60px #6F8CFF`, `filter: blur(.5px)`; in the live layer `from {scale:0, opacity:0} .3s back.out(1.6)`, then idle `y:"+=6" yoyo repeat`. In the UI layer, after the cut, `from {scale:.85} .4s power2.out` and the cloud texture slowly rotates (`rotation:20, duration:6`).

### 7.5 White-canvas UI with a pre-animated cursor
No device frames. UI panels sit on pure white at ~1.3x scale and are left-cropped (the panel bleeds off the right edge), so it reads as a zoomed crop. Sequence 18–26 s: sidebar (New chat / Pull requests / Scheduled / Plugins / Explore) → the cursor drifts to Plugins → the row highlights pale blue #DCE8FB with a blue dot → **zoom-cut** to the Plugins page (the title scales from 1.4x to 1x with a blur dissolve) → the search field types "Higgsfield" → the result row slides in with a **lime highlight sweep** behind it and an "Open plugin" black tooltip → Daily ad budget "$0" → the cursor clicks the "$200/day" chip (the chip fills light blue and the value **rolls 0→200**) → Target locations map with a blue radius circle pulsing around the truck pin, "3 km radius" tag, checkbox row.
Transitions between panels: ~250 ms **blur + scale dissolve** (outgoing scale 1→1.05, blur 0→8px, opacity →0; incoming scale .96→1, blur 8→0). Cursor: a black arrow with a slight motion trail, moves on eased curves (~400 ms, power2.inOut), and there is a 1-frame scale-down on click.
GSAP: `tl.to(cursor,{x,y,duration:.45,ease:"power2.inOut"}).to(cursor,{scale:.85,duration:.06,yoyo:true,repeat:1})`; panel swap `to(out,{scale:1.05,filter:"blur(8px)",opacity:0,duration:.25})` + `fromTo(in,{scale:.96,filter:"blur(8px)",opacity:0},{scale:1,filter:"blur(0)",opacity:1,duration:.3,ease:"power3.out"})`. Number roll: `gsap.to(obj,{v:200,duration:.5,ease:"power2.out",onUpdate:()=>el.textContent="$ "+Math.round(obj.v)})`.

### 7.6 Prompt send → output grid
A small composer card (image thumbnail + "Higgsfield" tag + prompt typed at ~25 chars/s + blue send button). Cursor clicks send (29.3) → a **blue pixel-shimmer sweeps left→right across the card** (29.6–30.1) → the card blurs and fades (30.2–30.5) → an "Opened Higgsfield" header writes in → a Posters panel with a 3x2 grid where **tiles fill one by one, ~120 ms apart, each blurring in from a grey placeholder** and a counter "1/6 → 6/6" ticking.
GSAP: shimmer = a gradient mask `background-position` sweep, .5s linear; tiles `from {opacity:0, filter:"blur(10px)", scale:.94} stagger:.12 ease:"power2.out"`.

### 7.7 Reel-card scroll + analysis callouts
Phone-shaped cards (radius ~24px, with an IG-like overlay: handle, views, caption, right action icons) **scroll vertically through a centred frame** with motion blur (37.3–37.9). They overshoot slightly and settle on one competitor reel, which then **scales up to bleed off the frame** (38.5–40.5, slow push ~1.15x). Blue pill callouts ("Analysing the content", "Learning the tags") **fly in from the edges, joined by thin 1px blue leader lines to points on the face/food**, with a cursor pointing at the target, and a rounded-rect outline highlighting the caption block.
GSAP: column `y` scroll `duration:.6 ease:"expo.out"` + `filter:blur(4px)` during the move; pills `from {x:±120, opacity:0} .35s power3.out`; leader line SVG `strokeDashoffset` draw .3s.

### 7.8 Pixel-regenerate swap. **Signature transition**
The competitor's reel turns into the chef's version: a **vertical band of green-tinted square pixels (~12px blocks) sweeps left→right** across the card over ~0.5 s (42.5–43.0). Behind the band the new footage (chef eating the burrito) is revealed. The overlay metadata switches to "@adilitos". The card then shrinks (43.2–43.6) and **flies out into a wall of scattered cards → snaps into a 3x3 grid** (44.0–45.5) of the chef's variants.
Rebuild: two stacked videos; a mask div with `clip-path: inset(0 X% 0 0)` animated 100→0 over .5s linear, plus a canvas layer of random squares (alpha .6, colour #9BE15D) living only in a 60px band at the mask edge. Grid: Flip-style `stagger:{from:"center",amount:.4}`, ease `power3.out`.

### 7.9 Live shot → card shrink (footage becomes the output)
53.5: the selfie shot (the chef points at the camera) gets a white flash wash for 1 frame (53.6). Then **the full frame shrinks to a rounded card** (53.7 ~85% → 54.1 ~25%), corners rounding 0→24px, with a soft blur on the first frames. Two sibling cards slide out from behind it to the left and right (54.1–54.3) to form a row of 3. The middle card then **pixel-regenerates** (green dither, 54.4–54.9) into a new UGC take.
GSAP: `to(video,{scale:.25,borderRadius:24,duration:.5,ease:"power3.inOut"})`; siblings `from {x:0, opacity:0} to {x:±170} .3s power2.out`.

### 7.10 Hooks Enhanced chip + regenerate row
A row of 3 cards; each card **dissolves to a new take** (cross-dissolve with a slight green dither, ~150 ms per card, left→right). A small **lime pill chip "Hooks Enhanced"** pops in under the row (60.5, scale .6→1 with back.out), and green check dots appear at each card's corner.

### 7.11 Upload → Ad preview → Ads manager
The row slides left off-screen with blur. An empty "Ad preview" panel builds with a shimmer skeleton (62.4–62.6). **A card flies in from bottom-left with heavy motion blur, rotating −8°→0°** (62.8–63.1) and lands in the preview slot, then expands into an Instagram Reels mockup. The panel then shrinks to a thumbnail (64.2–64.4) that becomes the first row of an **Ads list (V01 Burrito UGC, V02 First bite reaction, V03 Meet Chef Adil, V04 Inside the burrito, V05 Giant burrito)**. Rows cascade in ~80 ms apart and their **toggles flip on one by one** (65.0–65.7).
GSAP: flying card `fromTo({x:-300,y:200,rotation:-12,filter:"blur(12px)"},{x:0,y:0,rotation:0,filter:"blur(0)",duration:.35,ease:"power3.out"})`; toggles `stagger:.12`.

### 7.12 View counter on a video corner
Close crop of a rounded video corner (bottom-left radius ~40px) with an eye icon + "129K" in white semibold ~60px with a slight glow. **The number counts 129K→333K over ~1.4 s** (roughly +20–40K per frame early, then slowing: ease-out). The video behind it changes once (sauce cup → apron).
GSAP: `to(o,{v:333,duration:1.4,ease:"power3.out",onUpdate:()=>t.textContent=Math.round(o.v)+"K"})`.

### 7.13 CTA slam "comment ADS"
71.0: small lowercase "comment" (extended bold, lime) writes in, mid-lower. At 71.2 **"ADS" in a huge extended black weight enters from a scale of ~1.1 with a strong blur (~10px) and settles to sharp by 71.4** (about 6 frames). Lime #D6F536 sits over the chef's torso with no box. A small white caption under it continues ("I'll send you / the full setup"). It holds to the end while the chef turns away to serve.
GSAP: `from(ads,{scale:1.12,filter:"blur(10px)",opacity:0,duration:.2,ease:"power4.out"})`.

---

## jungle 7.x

### 7.1 Title punch-through (00:00.0–00:02.3)
- The lockup blurs in (blur 12→0, opacity 0→1, 5 frames).
- The main title has a 1-frame LED/dot-matrix glitch smear, then resolves to chrome serif.
- The pill is stretched-in on X. The UI chips fade-rise.
- Hold 0.5 s, then the whole group scales 1→1.8 with blur over 3 frames while the background plate flies forward.
- Sticker flowers sit in the corners and parallax with the plate.

**GSAP:**
```js
tl.from('.lockup',{filter:'blur(12px)',opacity:0,x:-30,duration:.2,ease:'power2.out'})
  .from('.title',{scaleX:3,opacity:0,filter:'blur(8px) brightness(3)',duration:.12,ease:'expo.out'},.5) // add a dot-matrix overlay (radial-gradient dots mask) at opacity 1→0 over .1
  .to('.lockup',{y:-60,scale:.55,duration:.15,ease:'power2.out'},.5)
  .from('.pill',{scaleX:4,transformOrigin:'0 50%',filter:'blur(6px)',duration:.14,ease:'expo.out'},.85)
  .from('.chip',{opacity:0,y:6,stagger:.06,duration:.2},1.0)
  .to('.titleGroup',{scale:1.8,filter:'blur(24px)',opacity:0,duration:.14,ease:'power3.in'},2.0);
```

### 7.2 In-world notification bubble (00:08.3)
- A white rounded rect (radius about 10px, no shadow, about 18% of frame width) placed **beside the phone in the plate**, not at the screen edge.
- Tiny grey "Today 10:24" above it, "Client" label below-right.
- Text reveals line by line with a blur (the 2nd line "ASAP." blurs in about 4 frames after the 1st).
- The bubble stays fixed in screen space for about 3 s while the hero moves.

**GSAP:** `from('.bubble',{opacity:0,y:8,scale:.96,duration:.25,ease:'back.out(1.6)'})`, then `from('.line',{filter:'blur(6px)',opacity:0,stagger:.17,duration:.2})`.

### 7.3 Floating dialogue words (00:13.8–00:19.3, 00:39.6)
- Spoken lines appear as **2–3 word fragments in white bold sans** (Inter-like, weight 600). They are scattered in a loose diagonal cluster near the speaker's head, each word at a slightly different size/opacity.
- Each word blurs in (blur 10→0, about 5 frames) and blurs out while the next appears. Max 3 words visible at once, with previous words fading to about 30% and blurred (a depth-of-field feel).
- This replaces subtitles while keeping the frame cinematic.

**GSAP:** for each word `fromTo(w,{opacity:0,filter:'blur(10px)',y:6},{opacity:1,filter:'blur(0)',y:0,duration:.2})`, then `.to(w,{opacity:.3,filter:'blur(4px)',duration:.3},'+=.25')`, then exit `opacity:0`.

### 7.4 Pixel mascot morph (00:13–00:21)
- The cat is a pixel sprite with a 1px darker outline. It is **not tracked to the log**; it floats in screen space with a gentle 2–3 px bob.
- Morphs are **hard cuts between sprite states** (cat → cube → triangle → fire → code text → cat), each held about 0.6–0.8 s and synced to the floating word ("Objects?" / "Shapes?" / "VFX?" / "Expressions?").
- The fire state adds an emissive glow that tints the whole plate (an orange overlay at about 40% plus a bloom), then breaks into pixel embers that rise and fade.
- The code state is pixel-font yellow text "time * 60 / wiggle(2,10)".

**Rebuild:** a CSS sprite stack with `steps()` swaps. Fire = sprite + an overlay `div` with `mix-blend-mode:screen; background:radial-gradient(#ff7a1a,transparent)`, tweened opacity 0→.6→0 over 0.6 s. Embers = 20 small squares with `y:-80, opacity:0` randomised over 0.8 s.

### 7.5 Prompt bar (the core recurring UI) (00:19.6, 00:29, 00:38, 00:53, 00:61)
- **Look:** a dark glass bar (about 45% of frame width, about 10% height), fill rgba(18,18,20,.72) with backdrop blur, radius about 14px. A **thin warm-orange inner glow on the bottom edge** (#E8734A at about 35%). Content: "+" at left, "Opus 5.5" label, mic icon, and an orange circular send button (#E8734A) with a white up-arrow.
- **Placement:** it moves per shot to the empty side of the composition (bottom-right at 00:20, bottom-left at 00:29/00:54/00:61, right at 00:38), never covering the face.
- **Entrance:** it fades up from blur in about 6 frames, empty.
- **Typing:** the text types at about 18–22 chars/s. The **newest 3–4 characters are coloured orange** (#E8734A) and fade to white, a "hot cursor" trail.
- **Send:** the send button blooms (an orange radial glow 3x its size, about 4 frames). Then the **bar pixel-dissolves into orange squares from the button leftward** (blocks about 2.5% of bar width, 4–6 frames). Then a hard cut.

**GSAP:**
```js
// type: split chars, each char from color:'#E8734A' to '#fff' over .25s, stagger .05
tl.to('.send',{boxShadow:'0 0 40px 18px rgba(232,115,74,.8)',scale:1.15,duration:.12,yoyo:true,repeat:1})
  .to('.bar .px',{opacity:1,stagger:{each:.01,from:'end'},duration:.05})  // grid of orange squares over bar
  .to('.bar',{opacity:0,duration:.08});
```

### 7.6 White "agent status" card (00:22.0, 00:31.0, 00:41.9, 00:45.4, 00:63.5)
- **Look:** a full-frame flat light grey (#F5F4F8), no frame or device. Left-aligned text block, vertically centred, beginning at about 40% of frame width. A Claude-orange asterisk icon left of the text (about 1.5x cap height).
- **Copy pattern:** line 1 is a bold-ish dark statement; line 2 is a lighter sub-line. When Higgsfield is acting, a lime #D4F01E rounded-square app icon is shown with a pink-magenta (#C2185B) line, "Generating visuals for 'Ivayu' Reserve."
- **Animation:**
  - The icon blurs in first (1 frame lead).
  - The text appears **word-by-word with blur** (blur 8→0, about 3 frames per word).
  - Then there is a **grey→black colour sweep left to right**, like LLM streaming: words arrive at #B5B5B5 and darken to #1A1A1A about 0.25 s later.
  - The block drifts (scale 1.0→1.03 or a 20px horizontal drift) over its 1.25 s life.
  - Exit is a hard cut, or blur-out at 00:43.0.
- **Variant 00:63.5:** a file chip (Ae icon, "Ivayu Reserve Promo / After Effects", "Download ⌄" button), soft grey fill #E4E3E8. It enters with blur and lands, with a small horizontal drift.

**GSAP:** words `from({opacity:0,filter:'blur(8px)',x:-4,stagger:.06,duration:.15})` plus `to({color:'#1A1A1A',stagger:.06,duration:.2},'<.2')`, with the card group `fromTo({scale:1},{scale:1.03,duration:1.3,ease:'none'})`.

### 7.7 Pixel-glow reveal of a generated asset (00:23.5–00:24.3, 00:55.0–00:55.7)
- Inside AE, a placeholder (a green star badge, or an empty stepped photo frame) gets a **ring of glowing lime-yellow pixel blocks** (#D8F03C core, soft bloom). The ring starts at the centre and expands outward to the frame edge in about 0.4–0.6 s.
- Behind the ring, the generated image is revealed (a circular mask whose edge is pixelated). This is "Higgsfield generating".
- The frame is a **stepped/notched polygon** (pixel-staircase corners) with a 3px white stroke.

**Rebuild:** `clip-path: circle(r at 50% 50%)` tweened r 0→75%, plus a canvas or SVG ring of 8px squares on the clip edge with `filter: drop-shadow(0 0 8px #D8F03C)`. Ease `power2.out`, 0.5 s. Use a stepped polygon `clip-path` for the frame.

### 7.8 Asset-board build (00:46.7–00:49.6, 00:56.5–00:59.6)
- Photo cards pop around the map one at a time, about 0.35 s apart, each with the same stepped frame. Each starts as an **empty dashed selection box with corner handles** (AE transform box), then the pixel-glow fills it.
- Labels (dark-green pill, white caps, e.g. "PARROT FALLS") slide in under the photo.
- The poster headline "THE SUN GATE" types in **letter by letter with a text cursor bar** (00:56.6 "TH|"), in a chunky cream (#F4ECD6) display sans (Archivo Black-like, all caps, tight leading).
- Pills (pink/yellow/white: "2.4 km", "SUNSET 18:40") pop with overshoot.
- The real cursor is visible and clicks each slot right before it fills. This sells "a user is directing it".

### 7.9 Screen ↔ world match transition (00:27.5 → 00:28.0)
- The AE comp viewer shows the hero (generated footage) in the jungle. He **runs out of frame-right inside the comp** (motion blur).
- Cut to the live full-frame shot of him running in the same jungle, same direction. The UI becomes the world.

**Rebuild:** end the UI shot on a video element inside a mock window where the subject exits screen-right. Cut on motion to a full-bleed clip with the subject entering from screen-left. Keep the direction consistent.

### 7.10 Window as object (00:32.5)
- The AE project panel is shown as a floating macOS window over a **blue-sky background** (not the desktop). It slides up from the bottom with motion blur (about 6 frames), then the camera pushes into the folder list.
- The list items reveal top-to-bottom (folders expand to show files).

**Rebuild:** a window div `from({y:'60vh',filter:'blur(10px)',duration:.25,ease:'expo.out'})`, rows `from({opacity:0,x:-8,stagger:.05})`.

### 7.11 Whip-pan inside UI (00:34.5–00:35.0)
- A horizontal smear (motion blur about 40px) from the comp viewer to the timeline. The timeline then slowly scrolls/pushes to show dense keyframe diamonds on coloured layer bars (green, blue, red, orange, pink).

**Rebuild:** `x:'-100%'` with `filter:blur(30px)` over 0.2 s `power4.inOut`, plus a slow `scale 1→1.1` on the timeline.

---

## API apps 7.x

### 7.1 Lime-ink text reveal (signature, used on every AI line)
- Text writes on left->right per character. The newest ~6-10 characters are **acid lime (#C8FF3A) and slightly blurred/low opacity**. Behind the "ink head" they settle to final grey #5A5A60 (or near-black for bold lines). It looks like wet ink drying.
- Speed ~25-35 chars/s (e.g. "The solution: build your own AI apps with the Higgsfield API." ≈ 60 chars in ~1.7 s).
- Often paired with a **camera pull-back**: the line starts as a huge macro (focus blur) and ends as a small centred line (18.7->20.0, 26->28).
- **GSAP:** split into chars; `tl.from(chars,{opacity:0,filter:'blur(4px)',color:'#C8FF3A',duration:0.35,stagger:0.03,ease:'power2.out'})` then `tl.to(chars,{color:'#5A5A60',duration:0.4,stagger:0.03},'<0.25')`. Container: `fromTo(scale 3.2, blur 8px -> scale 1, blur 0, 1.4s, expo.out)`.

### 7.2 "Thinking" label shimmer
- OpenAI knot icon + "Intently thinking" in grey 40% size of the screen. A **light gradient sweeps** across the letters (the "thin**k**ing" highlight moves). It scales from slight blur at 7.4 s to sharp at 8.1 s, then the camera pulls back so the label becomes a small header above the answer (8.9 s).
- **GSAP:** `background: linear-gradient(90deg,#8a8a90 40%,#d8d8de 50%,#8a8a90 60%); background-size:200%; -webkit-background-clip:text;` tween `backgroundPosition '200%'->'-200%'`, 1.2 s, linear, repeat.

### 7.3 Prompt card + pixel-burst send (motif x5)
- The card is a white pill (radius ~24 px) with a long soft shadow `0 30px 60px rgba(0,0,0,.12)`, "+" at left, "◎ GPT-6 Astra" and a round send button at right. It floats in 3/4 perspective (rotateY ~-8°).
- The text types in with lime ink (7.1). On send: the button goes **black -> blue gradient (#3D7BFF->#6FA8FF)** with an outer glow, then **pixel squares** (8-24 px, blue/cyan, 20-60% opacity) scatter outward and up-left over ~6 frames. The background flashes pale blue (#DCE9FF) for 2-3 frames, then the next scene.
- **GSAP:** button `to({background:'#3D7BFF',boxShadow:'0 0 30px #6FA8FF',scale:1.08},0.12)`; spawn 30 divs at the button centre; `to(px,{x:rand(-300,60),y:rand(-200,80),opacity:0,scale:rand(.5,1.6),duration:0.35,ease:'power3.out',stagger:0.005})`; overlay `#DCE9FF` opacity 0->.6->0 in 0.15 s.

### 7.4 Pixel-mosaic assemble / dissolve (UI element build)
- Used for the API chip (16.75-17.25), wireframe app parts (40-45: buttons, text fields, the "+" tile) and blur transitions. Elements appear as a **coarse block mosaic with RGB-fringed noise edges** that resolves to sharp within ~8-12 frames. The dissolve-out runs it in reverse.
- **Rebuild:** a canvas mask of NxN blocks revealed in random order (or CSS `clip-path` on a grid of tiles) + `filter: blur(6px)->0` + a slight `scale 0.96->1`, 0.45 s, steps(10) on the mask and expo.out on blur.

### 7.5 Logo stroke write-on on a colour flood
- Full-frame lime (#C8FF3A with a subtle radial lighter centre). The black brand mark is **drawn as a thick stroke** whose leading edge has a motion-blur feather. ~0.85 s, ease-in-out, then the whole frame scales down so the logo becomes a 48 px rounded-square badge on white (15.0-15.25).
- **GSAP/SVG:** `strokeDasharray` draw 0->100% in 0.8 s `power2.inOut`; then `to(stage,{scale:0.08, borderRadius:'22%', duration:0.3, ease:'expo.in'})` and the white bg fades in behind.

### 7.6 Glowing product chip
- Rounded square ~260 px. Dark olive face with a lime gradient from the bottom-left corner (#E4FF4A -> #2A3010), embossed letters "HIGGSFIELD / {API}", a small port dot, a **lime neon rim** (`box-shadow: 0 0 0 3px #D7FF3A, 0 0 40px #B8F03C88`). Slow yaw ±10° and pitch 5° over 1.5 s on black.
- Variants: plugged in with 6 glowing bezier cables (46.5); node-graph hub (62-69).
- **Rebuild:** CSS 3D `perspective:1200px; rotateY` loop, `sine.inOut`, 1.6 s yoyo.

### 7.7 App-store scan + highlight blobs (research montage)
- A real-looking App Store "Create" page (sidebar + 3-column grid). Cards get covered by **blurred lime and pink/lilac gradient blobs** that sweep across like a heatmap scan (31-33), then fade back to the icons. The camera pulls out to ~40% size and the window rises as a checklist builds below it.
- Checklist items: OpenAI icon + grey line, each typed with lime ink, new line every ~1.2 s. Older lines blur slightly as new ones come in (depth-of-field fake).
- **Rebuild:** for each card, an absolutely positioned `div` with `background: radial-gradient(#C8FF3A, #F0A8FF, transparent)`, `filter: blur(18px)`, `opacity 0->.9->0`, stagger 0.04, 0.8 s.

### 7.8 Wireframe -> styled app ("it's built" reveal)
- The app first appears as **flat grey (#8E8E93) blocks** (title, black media tile with a "+", input pill, black CTA "Generate video ->"), each pixel-assembled. The camera hugs it in tilted close-ups.
- The orbit behind the device (see 7.6) returns to the front with the app now themed: cream card, magenta media tile, lime CTA, all on a pink/lime **aurora blur background** (big soft radial blobs #F07BE0 and #E6FF8A on #FAF8F5).
- Then a real demo: the vase photo fills the media tile, a "Styles · 5 seconds · 9:16" thumbnail strip highlights the selected thumb with a pink glow, and the output video scales out of the card to fill most of the frame. The camera pushes into a macro of the glaze texture (proof of quality).
- **Rebuild:** two DOM states; `gsap.to(card,{rotateY:180,duration:0.9,ease:'power3.inOut'})` with the backface showing the chip; on return, swap to the styled state with a crossfade.

### 7.9 Node graph (one engine, many products)
- Dark bg (#0B0D05) with a lime ground-glow from the bottom. The chip sits at the centre and 4 app screens sit around it at different sizes (phone, web, phone, desktop). They are joined by **orthogonal circuit traces** (2 px lime #C8FF3A + 8 px glow) with right-angle bends.
- Build order: web app first (61.0) -> pull back -> other screens slide in from off-frame with motion blur (62.5-63.0) -> traces draw out from the chip (stroke-dash, 0.4 s).
- **Deploy burst (68.4-68.7):** square pixel particles (lime, 4-16 px) erupt from the chip radially, fill the frame and fade. Then the screens **shrink into app icons** (heart, cat, H, house) orbiting the chip, and the camera dives past them (motion blur) into the next scene.

### 7.10 App-store rank climb
- A "Top Apps" list (rows: icon, rank number, name, sub, "Get" pill) seen in **steep 3D perspective** (rotateX ~35°, rotateZ ~-6°), scrolling up fast with motion blur.
- The hero's apps are **lime-outlined, glowing cards that float above the list (translateZ)** and move up faster than the list, passing other rows: 10 -> 4 -> 2 -> 1. The camera flattens to front-on at 72.8. "Lovestory Studio" locks into row 1 with a lime outline (`box-shadow 0 0 0 3px #D7FF3A, 0 0 24px #C8FF3A`). PETMANGA sits at #4/#5.
- **Rebuild:** list `rotateX(35deg)` -> `0` over 2.5 s `power3.out` while `y` scrolls; hero card `y` tween with `expo.out` and `scale 1.04->1`; row swap with FLIP.

### 7.11 Live <-> UI transitions
- UI -> live is always a **hard cut on a send/decision**. Live -> UI is a hard cut too. No screen-inside-laptop shots: the laptop is **never shown with the UI on it** (the lid is always toward camera or the shot is on the hands/keys). The UI is "his mind/screen" as a separate space.
- Behind-the-head time-skip: the camera orbits from profile to the back of the head (0.5 s), the frame goes fully dark for ~5 frames, and it emerges from behind a different head/outfit in the new location. Do this in AI video by generating two shots: A ends with the camera passing behind the head into darkness, B starts in darkness behind the head; join them with a 3-frame black.

## Katana 7.x

### 7.1 Outline-to-fill verdict word
- Word appears as 2 px white stroke only for 3 frames, then fill snaps on, holds 2 frames, cuts out. No movement. Total 10 frames.
- GSAP: `set(el,{opacity:1, color:'transparent', webkitTextStroke:'2px #fff'})` at t; `set(el,{color:'#fff'}, t+0.125)`; `set(el,{opacity:0}, t+0.42)`. Font: Clash Display/Unbounded Bold, uppercase, 18% of frame height.

### 7.2 Red-dot power-up -> white flash -> ray burst -> logo glitch-resolve
- Red radial gradient dot (bloom) on a body part, scales 1->2.5 over 2 frames, frame turns white (1 frame), then warm radial ray burst (conic-gradient rays rotating 15 deg) for 2-3 frames, then logo over a red disc. Logo letters swap random glyphs for 6-8 frames before locking; secondary lines type on left->right.
- GSAP: dot `fromTo(scale:0.5→2.5, 0.08, 'power2.in')`; flash div `opacity 1` for 1/24 s; rays `fromTo(rotation:0→20, opacity:1→0, 0.12)`; text scramble (ScrambleTextPlugin, `chars:'upperCase', duration:0.35`); sub-lines `clipPath inset(0 100% 0 0 → 0 0 0 0), 0.2, 'none'`.

### 7.3 OFF -> ON mode toggle (signature device, used 6 times)
- Elements: label "OFF" (white bold caps) | pill (rounded rect, radius 30%, white) with black square knob (logo inside) on left. ON: knob slides right in 3 frames, pill floods neon yellow `#E4FF1A`, label becomes 2-line "KATANA / MODE". On the switch frame: horizontal motion blur + 3-4 white speed lines trailing left. Slight overshoot and 5 deg perspective tilt, settle 8 frames. Background footage dims/desaturates on OFF and comes back graded on ON.
- Size varies by context: hero size (about 30% width, centred) first time; compact lower-centre (about 15% width) later, so it becomes a recognisable glyph.
- GSAP: `tl.to(knob,{x:pillW-knobW, duration:0.125, ease:'power4.in'}).to(pill,{backgroundColor:'#E4FF1A', duration:0.04},'<0.08').to(pill,{filter:'blur(6px)', scaleX:1.15, duration:0.04},'<').to(pill,{filter:'blur(0)', scaleX:1, x:'+=8', rotationY:-6, duration:0.33, ease:'back.out(2)'})`; labels crossfade via `clipPath` wipe 0.08 s.

### 7.4 Footage -> UI glow match (orb transition)
- A glowing white orb is placed on the subject's back in the AI shot; camera zooms (radial zoom-blur) into it over 3 frames; it becomes an orange particle ring on a white app window that sits tilted in 3D on a pink gradient; the ring expands outward to the window edges (8 frames) revealing the UI (“Good day, Editor”), window then rotates to flat and scales up.
- GSAP: orb `scale 1→8, filter blur(0→20px), 0.12`; UI window `fromTo({rotationX:25, rotationY:-20, scale:0.7},{rotation:0, scale:1, duration:0.6, ease:'expo.out'})`; ring = radial-gradient mask `--r: 0%→140%, 0.35, 'power2.out'`.

### 7.5 UI whip-zoom navigation
- Between UI states, no cuts: the virtual camera whips (translate 30-60% of frame) with heavy directional blur (about 4-6 frames), lands with a soft ease, cursor already near target. Menu items are real UI, large on screen (zoomed 200-300%).
- GSAP: `to(stage,{x:-dx, y:-dy, scale:2.4, duration:0.25, ease:'expo.inOut'})` + SVG motion-blur filter tied to velocity (stdDeviation 0 -> 12 -> 0).

### 7.6 Chip write-on with light-bar wipe
- Inside a prompt card: icon tile pops with yellow-green glow (scale 0.6->1, 3 frames), then a vertical cyan/mint gradient bar (about 8% width, glowing) sweeps left->right across the row; text "Higgsfield Katana" is revealed behind it, letters first green-tinted then settle to black.
- GSAP: bar `fromTo(x:'-10%'→'110%', 0.3, 'power2.inOut')`; label `clipPath inset(0 100% 0 0)→inset(0 0% 0 0)` synced; `color '#9BFF5A'→'#111', 0.2`.

### 7.7 Image drop into prompt box
- Photo card (rounded, soft shadow) flies in from right, overshoots over the box at about 1.3x, then shrinks into a thumbnail slot top-left of the input (8-10 frames total), tilting slightly.
- GSAP: `from(img,{x:'60vw', rotation:6, scale:1.3, duration:0.35, ease:'power3.out'}).to(img,{scale:0.35, x:thumbX, y:thumbY, duration:0.3, ease:'expo.inOut'})`.

### 7.8 Typed prompt with colour-lagging caret
- Prompt types at about 12-15 chars/s; the most recent 3-4 characters are tinted brand red/orange and turn black as the next ones arrive ("Aura farming edit of my ca" with "ca" red).
- Implementation: render each char as span; new span `color:accent`, `gsap.to(span,{color:'#111', delay:0.2, duration:0.15})`.

### 7.9 Send-button ripple morph
- Orange send button glows, then concentric rounded-square outlines (4-5 rings) expand out from it in red/pink, with spiky splash particles; the button morphs into a pink gradient app-icon (Katana logo); text to its left pixel-dissolves. Then cut to footage. About 10 frames.
- GSAP: rings `fromTo(scale:1→4, opacity:1→0, stagger:0.04, duration:0.4, ease:'power2.out')`; icon `background` crossfade + `scale 1→1.15→1`.

### 7.10 URL -> chip collapse
- A long URL in an orange->magenta gradient pill slides in tilted (about -8 deg) with motion blur, then collapses horizontally into a short "🔗 link" chip, which settles in place; user keeps typing after it.
- GSAP: `from(urlPill,{x:200, rotation:-8, filter:'blur(8px)', duration:0.25})`, `to(urlPill,{width:chipW, duration:0.2, ease:'expo.in'})` while crossfading text to "link".

### 7.11 "Analyzing" scan across a profile grid
- Phone-profile grid zooms in; camera slides from photo to photo (about 0.7 s each); active photo lifts (scale 1.08), gets a glowing pink->yellow gradient border and a dark pill "◌ Analyzing..." with spinner; other photos dim to 60%.
- GSAP: loop over cells `to(cell,{scale:1.08, boxShadow:'0 0 30px #FF4FA3', duration:0.2})` + stage pan; spinner = CSS rotate.

### 7.12 Kinetic sentence, one word per beat
- Each word full-width, heavy italic grotesk caps, white, centred or lower-third, cut on every beat (0.25-0.5 s). Variations: stacked repeat "SPEED SPEED SPEED" with decreasing opacity; letters with subject masked in front (depth); text used as mask window ("GO" showing horse inside red letters); liquid/thermal displacement ("BLOOD"); 3D extrusion ("MY WIFE"); word strike-through scribble ("LOSER?"). Entry is usually a 1-2 frame blur-in or slight scale 1.1->1; exit is a hard cut.
- GSAP: per word `fromTo(w,{scale:1.12, filter:'blur(6px)', opacity:0},{scale:1, filter:'blur(0)', opacity:1, duration:0.06})` then `set(opacity:0)` on next beat. Persist a lower-third claim (e.g. "MAKE / ENGAGING EDITS") across many cuts for readability.

### 7.13 Persistent corner badge
- During the car edit, top-left badge: yellow rounded tile (Katana logo) + "MOTION / DESIGN" in white bold, with a magenta->yellow gradient glow behind. Stays fixed while footage cuts — tells you which feature is being shown.

### 7.14 Grade shifts as punctuation
- Toggling between full colour, B&W high-contrast, red duotone, invert/negative, thermal posterize. In CSS/canvas: `filter: grayscale(1) contrast(1.6)`; red duotone via SVG feColorMatrix; invert `filter:invert(1)` for 1-2 frames.

### 7.15 Letterbox tighten on climax
- Anime section: bars grow from about 1.78:1 to about 2.8:1 when Katana Mode switches on, signalling "cinema". Animate `height` of top/bottom bars 0 -> 18% over 0.3 s, `power3.out`.

## Lily's Pad 7.x

### 7.1 Word-append title card ("Introducing / Runway MCP in / Claude Opus")
- 04.07 black (#0B0B0B), "Introducing" in white, centred, about 6% of frame height, medium weight. Hard cut in, held 0.5 s.
- 04.57 cut to cream (#F5F4F0). Words are **appended one at a time** to a centred line, so the line re-centres and earlier words slide left each time: "Runway" (4.57) -> "Runway MCP" (4.82) -> "Runway MCP in" (5.2) -> replaced by "✳ Claude Opus 4.4" (5.4, with the orange Claude starburst glyph #D97757) -> the digits roll to "5.5" (5.5-5.85, vertical slot-machine flip, the old digit exits up and the new one enters from below, about 3 frames per digit). Text is **small** (about 3% of height) on the cream background. There is a very slow scale-up (about +5% over 1.5 s).
- **Rebuild (GSAP):** a flex row with `justify-content:center`; each word `span` starts `width:0; opacity:0`. Tween `width:auto, opacity:1, duration:0.18, ease:"power2.out"` every 0.25-0.35 s, so the centred row reflows smoothly. Digit roll: an overflow:hidden span with a stacked column [4,5]: `yPercent:-50, duration:0.25, ease:"power3.inOut"`, staggered 0.08 s between the two digits. Card: `scale 1 -> 1.05, duration:2, ease:"none"`.

### 7.2 Attachment drop-in (photo/logo/poster -> chat input)
- The tile (rounded square, radius about 18% of its width, soft shadow) enters **at about 1.3x size, from below-left, with a cursor attached**. It settles into the attachment slot by scaling 1.3 -> 1.0 and moving about 40 px up and right over about 0.5 s with ease-out (10.85-11.3, 21.9-22.5). The cursor keeps moving on afterwards (it drags on past). A second tile drops beside the first, and the row grows to the right.
- The camera is macro on the input box (the box is about 3x real size; only the "How can I help you t…" placeholder fragment is visible), so the UI reads as a physical object.
- **Rebuild:** `gsap.fromTo(tile,{scale:1.3,x:-40,y:60,boxShadow:"0 20px 40px rgba(0,0,0,.25)"},{scale:1,x:0,y:0,boxShadow:"0 2px 6px rgba(0,0,0,.08)",duration:0.5,ease:"back.out(1.2)"})`. Cursor: a separate SVG layer, same path, 0.1 s lead.

### 7.3 Typing with a following camera
- Text types at about 18-22 chars/s. The **newest characters fade in grey (about 40% opacity) and darken over about 3 frames**, as a soft trailing caret. The canvas **pans horizontally with the text end** so the last word sits at about 60% of frame width (11.3-12.2, 21.0-21.6). The line is never shown whole. Then a cut or a pan to the right end: "Opus 5.5 ⌄" plus the orange send button (#D97757, rounded square, white ↑). The cursor arrives and clicks (the button darkens about 10% for 2 frames).
- **Rebuild:** wrap the chars in spans with `opacity:0.35 -> 1, duration:0.1`, stagger 0.05 s. Animate container `x` = -(textWidth - 0.6*viewport) using `ease:"none"`, tied to the same timeline.

### 7.4 Generation card: placeholder -> progress -> blur-to-sharp reveal
- 13.1: zoomed out; a grey placeholder square (#EFEFEF) with "30%" centred in small grey text, plus a thin dark progress bar along its bottom edge that grows left-to-right over about 0.6 s. A tiny caption sits below ("Generating a dimensional unfolded stationery shop plan" in small serif grey) with 4 tiny dot icons.
- 14.1-14.4: the image **cross-fades in at about 20 px gaussian blur and sharpens to 0 over about 0.3 s**, while "30%" fades out. Then the action pills (black "Download", then "Animate" and "Edit" text buttons) fade in under the image (14.3-14.4).
- The merch version (28.33-28.8) is a 2x2 grid where **each tile un-blurs on a stagger** (top-left first, about 0.1 s apart), then the whole grid scales 1.0 -> 1.25 while a heading "Generate images and video" fades in above (29.6-29.8). That is a feature label delivered as UI.
- **Rebuild:** `tl.to(bar,{scaleX:1,transformOrigin:"left",duration:0.6,ease:"power1.inOut"}).fromTo(img,{filter:"blur(20px)",opacity:0},{filter:"blur(0px)",opacity:1,duration:0.35,ease:"power2.out"}).from(pills,{opacity:0,y:4,stagger:0.05,duration:0.2})`. Grid: `stagger:{each:0.1,from:"start"}`.

### 7.5 Output card -> live footage ("render becomes reality")
- 17.4-18.27: the result card (16:9 image with rounded corners on white) scales from about 45% of the frame width to about 90% in about 0.6 s (ease-in-out), corners still visible. At 18.27, a cut on motion to a live shot that starts **pointed up at the ceiling lamps of that exact room and tilts down** to reveal the heroine sitting on the floor in the generated space. The scale-up plus tilt reads as "diving into the picture".
- **Rebuild:** card `scale:0.45 -> 0.92, borderRadius:16 -> 8, duration:0.6, ease:"power2.inOut"` -> hard cut to a video clip that starts tilting (generate it with "camera starts on ceiling lamps, tilts down to reveal…"). For a seamless version, scale to 1.0 and fade the radius to 0, then cross-dissolve 4 frames.

### 7.6 Asset -> physical object match (logo -> iPad -> window)
- 23.67: hard cut from the send click to the same logo on an iPad (top-down). Push-in until the logo fills the frame (24.0-24.5), then a **6-frame cross-dissolve** from the logo artwork to the hand-painted frog on the shop glass (24.6-24.8). The frog face position is matched between the two shots (graphic match).
- **Rebuild:** align the logo centre in clip A and the painted logo in clip B. Opacity cross-fade 0.2 s while A keeps scaling (1.0 -> 1.15).

### 7.7 Spec overlay on live footage ("Access to all the latest models")
- 41.73-46.6: centred white thin sans text, about 2.5% of frame height, with no box, sitting over the street footage. Below it is a **2-row x 4-col grid of model chips** (icon + name, about 1.3% height, white at about 85%): Gen-4.5, Seedance 2.5, GPT Image 2.5, Kling 3.0 / Omni Flash, Nano Banana Pro, Gen-4 Image, Ruby. Static for 5 s, legible because the footage is busy but low-contrast. It is cut away rather than animated out. (The source text has a typo: "the the".)
- **Rebuild:** an absolutely positioned overlay with `text-shadow:0 1px 8px rgba(0,0,0,.35)`. Fade in 0.3 s, chips staggered 0.04 s. Hold, then hard cut.

### 7.8 End cards
- 50.43: black, centred white words, **one word replaces the previous one** ("Make" -> "anything" -> "from" -> "anywhere", about 0.25-0.3 s each, hard swap, no fade).
- 51.50: white, **left-aligned at about 11% x**, small black text typed word by word: "Now" -> "Now available" -> "…on" -> "…runway" -> "…runway.com" -> "…runway.com/mcp" (about 0.2-0.33 s per step, URL pieces appended as separate beats). Hold 0.7 s.
- 53.57: black, white bold lowercase "runway" wordmark, centred, 0.45 s, then black and silence.

## motion design 7.x

### 7.1 Cursor-built kinetic title
Lime arrow cursor drags a selection box, text types into it with chromatic blur, accent shapes (4-point stars) explode in from corners and bleed off-frame, cursor exits with smear.
**GSAP:** `cursor` x/y path 0→0.25 s `power3.out` + `filter: blur(6px)` during travel; `.box` scaleX 0→1 0.08 s; letters stagger 0.035 s from `{opacity:0, x:-8, filter:'blur(8px)', textShadow:'3px 0 #f0f,-3px 0 #0ff'}` to clean, `power2.out` 0.15 s; stars `scale:0.2,rotation:-30,opacity:0` → `scale:1, rotation:0` 0.35 s `back.out(1.8)` stagger 0.04; second line `y:30, filter:blur(10px)` → 0 in 0.2 s; whole group scale 1.04→1 0.3 s; cursor exit x:-600 0.3 s `power3.in`.

### 7.2 Prompt-bar push + whip
Bar wipes in with a moving gradient (cyan→lilac) that sweeps L→R then clears to white; camera punch-in to the left end; command chip appears; horizontal whip to the right end to land on the voice button.
**GSAP:** bar `clipPath: inset(0 100% 0 0)`→`inset(0 0 0 0)` 0.4 s `power2.out`, background-position 0%→100% simultaneously, then bg to #fff 0.2 s; stage `scale:1→2.2, x:+30%` 0.15 s `expo.out`; chip `opacity/blur(6px)`→clean 0.1 s; stage `x:-60%` 0.22 s `power4.inOut` with `filter:blur(12px)` peaking mid-move (use a horizontal SVG feGaussianBlur stdDeviation="20 0"); button pulse scale 1.12 0.15 s yoyo.

### 7.3 Voice orb + 2-line "teleprompter" caption (the system that carries the film)
Orb: ~90 px sphere, radial gradient #8B7BFF centre → #3D2BE0 edge, outer glow 40 px #5B4BFF @60 %, white sine-wave glyph in centre; enters from a 6 px dot at 0:05.27 to full in ~0.3 s with `back.out`, then breathes (scale 1↔1.06, glow pulses with VO amplitude). Sits in the room's negative space, left or right third, at head height.
Caption: 2 lines centred under orb, white SF-style regular ~26 px @1080p, no box, soft drop shadow. **Current line 100 % white, next line visible at ~35 % opacity below it.** When the speaker moves on, line 1 drops to 35 % and shifts up ~0.5 line; line 2 rises to 100 %. Crossfade ~0.25 s.
**GSAP:** `tl.to(l1,{opacity:.35,y:-14,duration:.25,ease:'power2.out'}).to(l2,{opacity:1,y:-14,duration:.25},'<')`. Orb `from({scale:0.07,opacity:0,duration:.3,ease:'back.out(2)'})`; idle `gsap.to(orb,{scale:1.06,repeat:-1,yoyo:true,duration:.6,ease:'sine.inOut'})`.

### 7.4 Reference-card attach
Above the chat bubble, 3 rounded image cards (radius 10, small × in corner) pop in L→R: first sharp, others arrive as blurred smudges then resolve (0:08.5-0:09.0), stagger ~0.12 s. Prompt text wraps word by word into a second line.
**GSAP:** cards `from({y:12, scale:.85, opacity:0, filter:'blur(10px)', stagger:.12, duration:.25, ease:'power3.out'})`.

### 7.5 Dock launch → app window zoom
Dock (glass pill) slides up from bottom 0.15 s, Ae icon does the macOS bounce (2 bounces, ~0.45 s), dock slides down, dark window scales out from the Dock position (scale 0.1→1, origin bottom-centre, 0.3 s) with heavy blur that clears at 0:13.6, then window drifts up/forward slowly.
**GSAP:** `icon` y: 0→-24→0→-12→0 `power1.inOut`; window `from({scale:.1, transformOrigin:'50% 100%', filter:'blur(20px)', opacity:.6, duration:.35, ease:'expo.out'})`, then `y:-20, scale:1.04` over 1 s linear.

### 7.6 Lime pixel-scan "AI is working" highlight (signature)
Each new row in a list is preceded by a lime #C6F23A highlight band made of a dot-matrix/halftone texture with soft feathered ends; it sweeps across the row L→R (~4 frames), the row text resolves behind it, band fades. Rows appear one every ~0.17 s, each one pushing the list down. Also used to dissolve-in files/folders and to rename messy file names (old name → scan → clean name).
**GSAP/CSS:** row `height:0→22px` 0.1 s; band = `div` with `background: radial-gradient(#C6F23A 35%,transparent 40%) 0 0/4px 4px` + `mask: linear-gradient(90deg,transparent,#000 20%,#000 80%,transparent)`; animate `x:-100%→100%` 0.15 s `power2.inOut`, opacity 1→0 last 0.08 s; row text `opacity 0→1` at 50 % of sweep. Stagger 0.17 s.

### 7.7 Timeline → output build
AE timeline with coloured layer bars (green, blue, red, orange, pink) shown tilted/perspective, camera dollies right along it, then cut to comp viewer where the design builds: outline strokes of the big "W" shape draw on (stroke-dashoffset), "ZAYRO" pops, "VENN" pops, gradient W fills sweep in from top, small text (wavu music logo, '26 Wrap, 14 MILLION, TOP-5 NEW, BEST ALBUM '26) appear one by one every ~0.15 s.
**GSAP:** stage `rotationX:25, rotationY:-12` → 0 over 0.6 s; SVG path `strokeDashoffset: len→0` 0.5 s; headline words `from({scale:1.3,opacity:0, duration:.12, ease:'power4.out'})`; gradient shape `clipPath inset(100% 0 0 0)→inset(0)` 0.3 s; meta labels stagger .15.

### 7.8 Halftone dissolve reveal (AI-generated image)
Generated image arrives as a cloud of glowing lime/white halftone dots over the area, dots coalesce into the photo of the rapper over ~0.5 s (0:25.1-0:25.6).
**Rebuild:** canvas or CSS mask with dot pattern; animate dot radius 0→full via `mask-size` while photo `opacity .3→1`, plus `filter: brightness(2)→1`. 0.5 s `power2.inOut`.

### 7.9 Sketch → colour
Grey pencil line art on white in AE viewer (0:36.9-0:37.2), then 1-frame pop to clean black-outline coloured character; next shot the character loops a dance on gradient brand bg with music notes bouncing.
**Rebuild:** two stacked images, swap at a beat with `opacity` hard cut + 1.03→1 scale settle 0.12 s.

### 7.10 Composited chat bubble in live footage
iMessage-style light grey bubble ("Can you make versions in different formats?", tiny "Today 10:24" above, "Client" below) appears in the room's empty wall space: starts as blurred smear sliding from left (0:44.3), resolves by 0:44.5. Then rests static (no tracking).
**GSAP:** `from({x:-40, scaleX:1.3, opacity:0, filter:'blur(12px)', duration:.25, ease:'expo.out'})`.

### 7.11 AI activity log card
Light chat card: "I've reviewed the animation. A few transitions need work." types out, under it a tool line "🔗 After Effects · Refining transition timing and easing" and a status "• Refining the transitions…" in grey; header "Working for 43s ›" ticks to 44s. Older lines above blur/fade upward.
**GSAP:** text typewriter 35 chars/s; previous items `y:-30, opacity:.3, filter:'blur(3px)'` 0.4 s; counter increment each second.

### 7.12 Multi-format reveal
Same banner shown as 16x9, then 9x16 (two variants), then 21x9, each in AE viewer, hard cuts ~0.5 s apart (0:53.5-0:55.0), then the 21x9 cuts to the same design on a real billboard.
**Rebuild:** one master layout component with aspect variants; cut, don't morph.

### 7.13 Localisation swap
Text strings and AE layer names change EN→JP in place with a short scan/flicker per string (0:64.5-0:67.0), layout re-flows.
**GSAP:** per string: `opacity 1→0 .05`, swap text, `opacity 0→1 .05` + lime scan (7.6).

### 7.14 Glitch → desktop deliverables
Layer rows smear into vertical streaks (datamosh) 0.2 s, cut to blurred wallpaper that racks into focus, three folders dissolve in L→R with the lime pixel effect, labels resolve.
**Rebuild:** `filter: url(#displace)` with feTurbulence baseFrequency 0 0.4 animated, then folder `from({opacity:0, filter:'blur(8px)', stagger:.13})`.

## motion-ref T1–T22

### T1. Notification burst from phone (UI cards pop out of device)
- **Where:** 00:00.8 (f17–24)
- **Frame by frame:** f17: one notification sits on the lock screen. f18: unchanged. f19: 3 cards jump out at once. One goes left (about 8% of frame width, over the cone toy), one up-left, one right onto the paper (about 10% of width). Cards scale about 1.0→1.25 and lift (drop-shadow offset grows). f20–21: about 3% overshoot past the rest point. f22: settled and static through f34.
- **Timing:** about 3 f out (125 ms) plus 2 f settle (83 ms), about 210 ms total
- **Easing:** strong back-out. Use `back.out(2.2)` or `cubic-bezier(.2,1.6,.4,1)`.
- **Stagger:** effectively 0 to 1 f; all three move together. The radial fan sells it, not the delay.
- **Layering:** cards sit above the phone and cast a soft shadow on the desk (shadow offset about 6 px, blur about 12 px). Cards are semi-transparent pink glass (bg about rgba(255,180,210,.75) with backdrop blur).
- **Rebuild:**
```js
// cards start stacked at the phone notification slot, scale .9, opacity 0 (the first one is already visible)
tl.to(".notif", { x:(i)=>[-110,-40,140][i], y:(i)=>[-10,-60,-20][i],
  rotation:(i)=>[-12,-6,8][i], scale:1.25, opacity:1,
  boxShadow:"0 14px 28px rgba(120,40,160,.35)",
  duration:0.21, ease:"back.out(2.2)", stagger:0.02 }, 0.79);
```

### T2. Jump-cut to "levitation" state (same scene, objects lifted into depth)
- **Where:** 00:01.46 (f34→f35) and again 00:02.29 (f55→56)
- **Frame by frame:** no in-between frames. Frame 34 is the flat top-down layout. Frame 35 is the same objects seen at a 3/4 angle, now hovering at different Z, paper crumpled, cards larger. After the cut the camera keeps drifting slowly (about 0.5% of frame per frame) so the shot never freezes.
- **Timing:** 0 f transition. Each state holds about 20 f (830 ms) before the next jump closer.
- **Easing:** none on the cut. The continuous drift is linear (`none`).
- **Layering:** 4 depth planes. Foreground (pencils, blurred, 4 to 6 px blur), mid (cards, sharp), phone, background desk (2 to 3 px blur).
- **Rebuild (2.5D):** two pre-built layouts of the same elements. At the cut, `gsap.set` every element to its "lifted" transform (`rotateX:35, rotateZ:-20, z:var`, per-layer blur). Run one slow `to()` on a wrapper (`x:-20, rotation:2, scale:1.04, duration:0.9, ease:"none"`). Chain 2 or 3 jump-cuts that each step about 30% closer (scale 1→1.3→1.7).

### T3. Whip-smear frame as a cut
- **Where:** 00:03.17 (f76). Variants at 00:09.0 (f216) and 00:11.5 (f276).
- **What happens:** a single frame of a heavily motion-blurred close-up (laptop logo at 45°) sits between two unrelated shots.
- **Timing:** 1 f (42 ms)
- **Rebuild:** insert a 1-frame div with the incoming hero element at `scale:2.2, rotation:-35`, `filter: blur(6px)`, plus an SVG `feGaussianBlur stdDeviation="30 0"` (directional). Hide it on the next frame with `tl.set(el,{autoAlpha:1},t); tl.set(el,{autoAlpha:0},t+1/24)`.

### T4. Hero object flies at camera (scale-through)
- **Where:** 00:04.0–00:05.0 (f96–120). Cursor-triangle tumbles off the desk toward the lens.
- **Frame by frame:** f96 triangle about 4% of frame height, mid-left. Growth is slow at first (f96–104 about 1.5x) and then accelerates (f104–120 about 4x). It rotates about 40° and moves down-left. Background stays bright and blurred.
- **Timing:** 24 f (1000 ms)
- **Easing:** accelerating, `power3.in` (perspective makes linear Z look like ease-in).
- **Layering:** a foreground paper sheet sweeps across f91–95 as a dark blurred occluder (about 30% of frame width), a natural "foreground wipe".
- **Rebuild:**
```js
tl.fromTo(".cursorTri",{scale:.4,x:0,y:0,rotation:0},
  {scale:6,x:-180,y:260,rotation:40,duration:1,ease:"power3.in"},4.0);
tl.fromTo(".fgPaper",{x:"110vw"},{x:"-60vw",duration:.21,ease:"none"},3.79); // blur(12px), opacity .9
```

### T5. Animated letterbox (cinemascope crush)
- **Where:** in 00:05.04–00:05.67 (f121–136). Out about 00:09.3 (f224–227).
- **Frame by frame:** black bars grow from 0 to 156 px each (21.8% of frame height top and bottom). The visible window ends at 405 px (3.15:1). Bars stay through the Publish macro and the "IT'S LIVE" shot.
- **Timing:** 15 f in (625 ms). About 4 f out, hidden under the flash transition.
- **Easing:** `power2.inOut`
- **Why:** it marks a "moment of truth" (the click and the launch) and makes the macro feel filmic.
- **Rebuild:** `tl.fromTo(".bar",{scaleY:0},{scaleY:1,duration:.625,ease:"power2.inOut"},5.04)` with `.bar{height:21.8%;background:#000;transform-origin:top|bottom}`.

### T6. Macro cursor click on a 3D button
- **Where:** 00:06.0–00:07.4 (f144–178)
- **Frame by frame:** f144–149: cursor-triangle glides in from the bottom-right, about 15% of frame width, and decelerates. f150–159: it rests on the button with a micro drift of about 1 px per frame. f160–164: the press. The button label goes from lilac (#c58bd8) to white-glow over 4 f, and the button face brightens (inner glow). f165–175: hold pressed. f176–179: the camera lifts away and the cursor recedes.
- **Timing:** approach 6 f (250 ms), dwell 10 f (420 ms), press 4 f (170 ms), hold 12 f (500 ms)
- **Easing:** approach `power3.out`. Press `power2.out`. The button has no squash (scale stays 1); the press reads only through brightness.
- **Layering:** depth of field. Keyboard in the foreground blurred, button sharp, laptop screen behind blurred. Fine glitter or noise on the cursor material.
- **Rebuild:**
```js
tl.from(".cursor",{x:220,y:90,duration:.25,ease:"power3.out"},6.0)
  .to(".btn .label",{color:"#fff",textShadow:"0 0 18px #fff",duration:.17,ease:"power2.out"},6.67)
  .to(".btn",{filter:"brightness(1.25)",duration:.17},"<");
```
Shoot it as a crop: scale the whole UI 2.5x and blur the non-button layers 4 px.

### T7. Speed-line stabs plus radial burst
- **Where:** speed lines 00:08.75–00:09.0 (f210–215). Radial burst 00:09.0–00:09.1 (f216–219). Again at 00:11.5 (f276–277) and 00:15.6 (f374–377).
- **Frame by frame:** white wedges (long thin triangles, 2 to 6 px thick, 10 to 25% of frame width) stab in from the left edge, 2 to 4 at a time, new positions every frame. Then a full radial starburst of 60 to 100 thin streaks from a centre point. The streaks are white plus pink/violet tinted and hold for 2 to 4 f.
- **Timing:** speed lines 6 f. Burst 2 to 4 f. Positions are re-randomised every frame (on-ones).
- **Easing:** none. Each frame is a new random set, anime-style.
- **Rebuild:** a canvas or SVG layer. On each 1/24 s step draw N random wedges, seeded so the render is deterministic:
```js
for(let f=0;f<6;f++) tl.call(()=>drawWedges(seed+f, {from:"left", n:4}), null, 8.75+f/24);
// burst: 80 lines from (cx,cy), angle i*4.5deg+rand, length rand(.3,.9)*diag, stroke 2-5px
```

### T8. Posterised colour-flash frames (inverted / duotone hits)
- **Where:** 00:09.17–00:09.29 (f220–223), 00:11.33–00:11.46 (f272–275), 00:15.5–00:15.67 (f372–376), 00:21.5–00:21.96 (f516–527)
- **Frame by frame:** the outgoing or incoming frame is shown 1 or 2 frames at a time as a hard-contrast duotone: magenta #DB1AE6/#EF24EE, pink, violet #715DF9 with cyan #55A5F2 streaks. There is a coarse halftone dot overlay and a "paint smear" (dry-brush stroke) overlay. The colour scheme changes every frame. At f374 the starburst is cyan on violet; at f375 it is magenta on white.
- **Timing:** 4 to 6 f total, each state 1 to 2 f (42 to 83 ms)
- **Rebuild (CSS):** on the hero layer, per frame: `filter: grayscale(1) contrast(3) ` plus a coloured overlay div with `mix-blend-mode: color` (or `screen`), switching between #EF24EE, #715DF9 and #FFFFFF. Add a halftone PNG at `mix-blend-mode: multiply; opacity:.6`. Drive it with `tl.set` at 1/24 s steps. Never tween it.

### T9. Inset panel expands to full frame (window-reveal)
- **Where:** 00:15.75–00:15.9 (f378–381)
- **Frame by frame:** the new sky scene appears as a rectangle about 50% of frame height on white. It grows to full frame over 4 f, expanding mostly downward and rightward. A hot-pink hairline draws at the same time: an arc on the left plus a horizontal underline, about 3 px, gone by f380.
- **Timing:** 4 f (170 ms)
- **Easing:** `expo.out`
- **Rebuild:** `tl.fromTo(".scene",{clipPath:"inset(22% 0 28% 0)"},{clipPath:"inset(0% 0 0% 0)",duration:.17,ease:"expo.out"},15.75)` plus an SVG path with `strokeDashoffset` 100%→0→fade over 3 f.

### T10. Word "Answers": letter flicker, then scale snap, sandwiched behind the hero object
- **Where:** 00:15.8–00:17.2 (f379–414)
- **Frame by frame:** f379–385: the word is small (about 13% of frame width). Each frame one or two letters flip to hot pink (#EE2C76) at random (A, s, s, r…). f386: hard snap to about 2.3x size (about 33% of width), no in-betweens. f390: small pink sub-labels "easy" and "workflows" pop under it (2 f). f387–409: hold, with the umbrella floating in front of the middle letters (text behind object). f410–414: the word turns to a white outline and expands about 10%, then the letters drift apart ("swe…rs"), then gone.
- **Timing:** flicker 7 f, snap 0 f, hold 23 f (about 960 ms), exit 5 f
- **Rebuild:**
```js
const L = split(".answers");             // chars
for(let f=0;f<7;f++) tl.set(L,{color:i=>rand(seed+f*7+i)<.2?"#EE2C76":"#fff"},15.79+f/24);
tl.set(".answers",{scale:2.3},16.08)       // hard snap
  .from(".sub",{scale:0,duration:.08,ease:"back.out(3)",stagger:.04},16.25)
  .to(".answers",{color:"transparent",webkitTextStroke:"1.5px #fff",scale:1.1,letterSpacing:"0.2em",duration:.2},17.08)
  .to(".answers",{autoAlpha:0,duration:.08},17.25);
// z-order: sky < .answers < umbrella.png
```

### T11. Bottom panel slide-up plus word-type with highlight flash
- **Where:** panel 00:17.3–00:17.45 (f415–418). Typing 00:17.4–00:18.0 (f417–432).
- **Frame by frame:** a white panel slides up from the bottom to about 37% of frame height in 4 f (`expo.out`), with a slight blur on the leading frames. Headline words arrive one at a time. Each new word appears in hot pink (or as scrambled doubled glyphs: "course" shows as "cou**r**se"/"ccoouurrssee" for 1 f), and the previous word turns navy. Spacing: One f417, course f420–421, Teaches f422, Full f424 (pink) → navy f425, Production f427 (pink, scrambled) → navy f429. The bullet list on the right and the 3 thumbnails are already in place when the panel lands; they move with the panel.
- **Timing:** about 2 to 3 f per word (90 to 125 ms). The colour flash lasts 1 to 2 f per word.
- **Rebuild:**
```js
tl.from(".panel",{yPercent:100,duration:.17,ease:"expo.out"},17.3);
words.forEach((w,i)=>{ const t=17.4+i*0.11;
  tl.set(w,{autoAlpha:1,color:"#EE2C76"},t).set(w,{color:"#1B1A3D"},t+0.07); });
```

### T12. Giant ring sweep plus letter reveal behind a 3D object
- **Where:** 00:18.6–00:19.7 (f446–472)
- **Frame by frame:** f446–447: folder alone on off-white, slightly tilted (−20°). f448: a huge hot-pink brush-textured ring (stroke about 7% of frame width, halftone texture, diameter about 160% of frame height) slams in, cropping off-frame. It rotates about 6 to 10° per frame and keeps orbiting through f470. f449–456: "everything" reveals left to right, one letter every 1 to 1.5 f. Each new letter is hot pink and fades to pale pink #F7C9D8 about 3 f later, so a bright "head" travels along the word. The folder sits in front of the middle letters. The folder rotates from −20° to 0° over f446–456 (`power2.out`).
- **Timing:** ring in 2 f. Text 8 f for 10 letters. Folder settle 10 f.
- **Rebuild:**
```js
tl.fromTo(".ring",{scale:.6,rotation:-60,autoAlpha:0},{scale:1,rotation:0,autoAlpha:1,duration:.08,ease:"power4.out"},18.67)
  .to(".ring",{rotation:220,duration:1.1,ease:"none"},18.75);
tl.fromTo(chars,{autoAlpha:0,color:"#EE2C76"},{autoAlpha:1,duration:.01,stagger:.05},18.71)
  .to(chars,{color:"#F7C9D8",duration:.12,stagger:.05},18.83);
// ring: SVG circle stroke=#EE2C76, stroke-width 90, mask with halftone pattern
```

### T13. Container "spits out" contents (files pop from folder, then fan out)
- **Where:** 00:19.0–00:20.3 (f457–487)
- **Frame by frame:** f457–463: two file sheets (".aep", ".blend") rise out of the folder about 8% of frame height, staggered by 3 f, each with a small overshoot. f473: the folder front flap drops away (down-left, rotating) and the sheets become coloured cards (gradient pink/blue/lilac). f474–484: the cards fan up and to the right, spreading about 15% of width with a stagger of about 2 f. f485–487: everything stretches into one horizontal smear (motion blur about 20% of width) moving right.
- **Easing:** pop `back.out(1.8)`. Fan `power2.out`. Smear exit `power4.in`.

### T14. Motion-smear resolve into a UI strip
- **Where:** 00:20.33–00:20.46 (f488–491)
- **Frame by frame:** a horizontal band of blurred colour (grey, magenta, pink) about 35% of width, with a white swoosh arc under it. Over 3 f it sharpens into 5 to 6 video thumbnails (each about 5% of width), then stays. A pink leading block sits at the left edge for 2 f, then fades.
- **Timing:** 3 f resolve (125 ms)
- **Rebuild:** `tl.fromTo(".strip",{filter:"blur(14px)",scaleX:1.4,x:-120},{filter:"blur(0px)",scaleX:1,x:0,duration:.13,ease:"expo.out"},20.33)`. Use an SVG directional blur for a horizontal-only smear.

### T15. Pill tags pop in sequence
- **Where:** 00:20.75–00:21.25 (f498–510)
- **Frame by frame:** the blue pills (#2E8BC0 range, white label) under "Go beyond tutorials." appear one at a time: 3D f498, 2D f500, VO Edit f502, Composite f503, Sound design f506. The last one arrives as a blurred streak sliding in from the right (about 3% of width) and sharpens in 2 f.
- **Stagger:** 2 to 3 f (83 to 125 ms)
- **Rebuild:** `tl.from(".pill",{scale:.4,autoAlpha:0,duration:.1,ease:"back.out(2.5)",stagger:.1},20.75)`

### T16. 1-frame colour strobe on a single word
- **Where:** 00:21.5–00:22.1 (f516–530), word "start!!!!"
- **Frame by frame:** the background changes every frame: white, light pink, pink #E07FC0, violet #8D7DF9 (with outlined text), white, mauve, white, pink sketch texture, white… The word swaps between navy, white, hot pink and outline, and its "!" count changes (3, 4 or 5). It settles on navy text on white at f527.
- **Timing:** 11 f strobe (460 ms), then a 3 f hold
- **Rebuild:** an array of `{bg, color, text}` states applied with `tl.set` every 1/24 s. Respect photosensitivity: keep it under 3 full-field luminance flips per second, or use hue changes at similar luminance.

### T17. Shuttle square recolours a word ("Building")
- **Where:** 00:21.96–00:22.5 (f527–540)
- **Frame by frame:** f527: a rounded hot-pink square (about 2.2% of width) enters from the right edge next to "start!!!!". f528–530: it travels left (about 6% of width per frame). f531: cut to the off-white bg, word "Building" in hot pink with the square at its right. f532: the square is inside the word, and the letters to its right are navy while the ones to its left are still pink (a hard colour wipe at the square's x). f533: the square is just left of the word, now fully navy. f534–540: the square drifts left and the word drifts right (they separate by about 6% of width over 7 f, `power2.out`). The pair also slides right about 2% overall. Text: "Building", geometric grotesk semibold, about 5.8% of frame height.
- **Rebuild:**
```js
// word has two stacked copies: pink on top, clip-path driven by square x
tl.fromTo(".sq",{x:"60vw"},{x:"-9vw",duration:.25,ease:"power2.in"},21.96)
  .fromTo(".word .pink",{clipPath:"inset(0 0 0 0)"},{clipPath:"inset(0 100% 0 0)",duration:.08,ease:"none"},22.17)
  .to(".sq",{x:"-=4vw",duration:.3,ease:"power2.out"},22.25)
  .to(".word",{x:"+=4vw",duration:.3,ease:"power2.out"},22.25);
```

### T18. Giant cropped word slam plus drift ("Real")
- **Where:** 00:22.54–00:23.1 (f541–554)
- **Frame by frame:** f541: "R" enters from the right edge with about 20 px horizontal blur. Letters are 594 px tall, which is 83% of frame height. f542–544: the word travels left fast (about 25% of width per frame), decelerating. f544–554: slow drift left of about 1.5% of width per frame, still slightly blurred at the leading edge. The word is always cropped by the frame (bleeds off both sides).
- **Timing:** slam 3 f (125 ms), drift 10 f (420 ms)
- **Easing:** `expo.out` across the whole move (fast entry, long tail)
- **Rebuild:** `tl.fromTo(".real",{xPercent:80,filter:"blur(8px)"},{xPercent:-12,filter:"blur(0px)",duration:.55,ease:"expo.out"},22.54)` with `font-size:83vh; color:#EE2C76; letter-spacing:-0.04em`.

### T19. Word scale-collapse ("projects")
- **Where:** 00:23.13–00:23.33 (f555–560)
- **Frame by frame:** f555–556: "projects" large (about 30% of width), hot pink, centred on light grey #E4E1E5 (the bg also changes, from off-white to cool grey). f557: about 50%. f558: about 30%. f559: about 18%. f560: settled small (about 7% of width).
- **Timing:** 4 f (170 ms)
- **Easing:** `expo.out`
- **Rebuild:** `tl.fromTo(".projects",{scale:4.2},{scale:1,duration:.17,ease:"expo.out"},23.21)`

### T20. Comet stroke scatters letters, then draws the logo (logo outro)
- **Where:** 00:23.4–00:24.6 (f560–590)
- **Frame by frame:** f560–566: a short hot-pink brush stroke (rounded, gradient #F06A7A→#EE2C76) rises from below centre toward the word, growing from about 1% to 4% of frame height. f567: it hits "projects" and the letters burst outward (scattered, rotated ±60°, about 5% of width radius) with tiny white sparkle crosses. f568–571: the letters fade out over 4 f. f572–575: the stroke stands vertical, then bends into the first curve of the script "S". f576–584: it draws the full "S" with an overshoot wobble. f585–590: it draws "w" and the "SaaSWAVE" wordmark types underneath (about 6 chars per 2 f). In parallel at f565–567, a grey footer (#DAD4D8, bottom 25% of frame) slides up in 3 f with socials, "available now", the URL and tags.
- **Timing:** comet 6 f. Scatter 5 f. Logo draw 18 f (750 ms). Hold 41 f (1.7 s).
- **Easing:** comet `power2.in`. Scatter `power3.out`. Draw `power1.inOut` along the path.
- **Rebuild:** an SVG logo path with `stroke-dasharray`. Animate `strokeDashoffset: len→0` over .75 s. Letters scatter: `tl.to(chars,{x:()=>rand(-60,60),y:()=>rand(-40,40),rotation:()=>rand(-60,60),autoAlpha:0,duration:.2,ease:"power3.out"},23.92)`. Footer: `from({yPercent:100,duration:.12,ease:"expo.out"})`.

### T21. Ribbon unravel (logo becomes a flying 3D ribbon)
- **Where:** 00:11.6–00:14.3 (f278–343)
- **What:** the drawn logo on paper extrudes into a glossy red ribbon (f278–290, grows about 20% in scale), holds 10 f, then one end pulls right and the ribbon unwinds out of frame (f301–320) while the camera pushes in about 30%. Next shot: the ribbon streams left→right across a white void full of sticky notes at 3 parallax speeds (foreground notes about 3x the speed of the background).
- **HTML substitute:** one SVG path for the ribbon (stroke #D81E2C, width 14 px, with a lighter inner stroke for gloss). Animate the path `d` with MorphSVG, or animate `strokeDashoffset` while translating the whole SVG. Sticky notes are 3 layers with `x` tweens of 120 / 260 / 520 px over 1 s, `ease:"none"`.

### T22. Inflatable balloon type ("so" / "many")
- **Where:** 00:14.37–00:15.0 (f345–360)
- **What:** f345: "so" appears small and flat, white with a red outline. f346–351: it inflates into glossy red balloon letters (scale 1→2.4, `elastic`-ish wobble). f352: it cross-dissolves into "many" in pastel pink/lilac balloon letters that grow 1→1.3 over 4 f, then rest. Sticky notes stick to the letters.
- **HTML substitute:** a chunky rounded font (e.g. "Rubik Bubbles"/"Chango"-like) with a layered `text-shadow` stack for a puffy look plus a radial-gradient highlight via `background-clip:text`. `tl.from(word,{scale:.3,duration:.4,ease:"elastic.out(1,.45)"})`.

---

## motion-ref transitions X1–X19

| # | At | From → To | Type | Duration | Recipe |
|---|---|---|---|---|---|
| X1 | 00:01.46 | top-down → 3/4 levitation | Jump cut to the same set in a new depth state (T2) | 0 f | Swap layout transforms with `tl.set`; keep a constant drift on both sides of the cut |
| X2 | 00:02.29 | wide float → close card | Jump cut 30% closer on the same axis (a punch-in) | 0 f | `tl.set(stage,{scale:"*=1.35"})` |
| X3 | 00:03.17 | close card → office | 1-frame whip smear of the next hero (laptop logo) (T3) | 1 f | Smear frame, then the new scene |
| X4 | 00:03.8–00:04.0 | office (inside the shot) | Foreground occluder wipe (paper sheet crosses the lens) | 5 f | Blurred dark shape `x: 110vw→-60vw`, `ease:none` |
| X5 | 00:05.04 | office → laptop | Letterbox close plus dolly-in, then hard cuts to closer angles (f131, f136) | 15 f bars | T5 plus 2 punch-in cuts |
| X6 | 00:07.46 | Publish macro → "IT'S LIVE" | Hard cut on the button press, followed by an orbit move | 0 f | Cut on the action peak (the frame after the press) |
| X7 | 00:08.75–00:09.29 | live laptop → pen macro | Speed lines, then radial burst, then 4 duotone smear frames (T7+T8) | 13 f | Overlay layer on ones |
| X8 | 00:09.83–00:09.96 | inside pen shot | Hot-pink organic blob pokes in at top-left for 3 f | 3 f | SVG blob, `scale 0→1→0`, `ease:none` |
| X9 | 00:11.33–00:11.6 | pen macro → top-down paper | Magenta posterised frames, then a white radial burst with the marker as the shared centre | 6 f | T8, then T7 burst |
| X10 | 00:13.33 | top-down → ribbon void | Hard cut on the shared element (the red ribbon continues its direction left→right) | 0 f | Match cut on the motion vector |
| X11 | 00:15.0–00:15.46 | "many" → umbrella | Foreground hero rises and covers the frame (umbrella becomes the next shot's subject) | 11 f | Big blurred foreground object `y:100%→0` |
| X12 | 00:15.5–00:15.9 | balloon scene → sky | Duotone flash ×4 (magenta, pink, violet/cyan, magenta), white burst, inset panel expands (T8+T9). Umbrella stays centred throughout (shared element). | 10 f | As listed |
| X13 | 00:18.33–00:18.58 | sky → white folder | Cross-fade to white (sky fades over 6 f, umbrella dissolves) | 6 f | `autoAlpha` 1→0, `power1.in`, on a white bg |
| X14 | 00:20.1–00:20.46 | folder cards → UI | Cards smear right and resolve into the thumbnail strip (T13 into T14) | 6 f | Shared colour mass becomes the UI |
| X15 | 00:21.5 | UI → "start!!!!" | White flash frame (f516), then strobe | 1 f | `tl.set(white,{autoAlpha:1})` |
| X16 | 00:22.08 | "start" → "Building" | The pink square carries across the cut (shared element) | 0 f | Same square element persists |
| X17 | 00:22.54 | "Building" → "Real" | Hard cut, slam-in | 0 f | T18 |
| X18 | 00:23.13 | "Real" → "projects" | Hard cut plus bg change from warm off-white #F0EEEA to cool grey #E4E1E5 | 0 f | T19 |
| X19 | 00:23.4–00:24.6 | word → logo | Comet stroke morphs from the word into the logo (T20) | 30 f | As T20 |

**Pattern:** the 3D section uses match cuts and shared heroes (cursor-triangle, ribbon, umbrella). Every big location change is covered by a 4 to 13 f flash or burst, never by a dissolve. The type section is all hard cuts with one element carried across (the square, the comet).

---
