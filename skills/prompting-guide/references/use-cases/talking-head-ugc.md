# Talking heads, UGC, lip-sync, a character's voiceover

Markers: **[tested]** = generated and reviewed in a source test reel. **[untested]** = not run in a source test. Unmarked = the source gave no status (the UGC genre templates below are unmarked).

## Triggers

"talking head", "make my avatar talk", "AI spokesperson", "UGC ad", "creator-style video", "TikTok-style ad", "lip-sync", "say this line", "voiceover from the character", "testimonial", "unboxing video", "GRWM", "street interview", "the line got cut off", "the voice changes between clips".

## Load these

| Need | File |
|---|---|
| The person (identity still, realism, consent) | [avatar-portrait.md](avatar-portrait.md) |
| Same person across clips | [character-consistency.md](character-consistency.md) |
| Phone-footage look (crisp, handheld, 30 fps) | [../styles/motion-shutter.md](../styles/motion-shutter.md) "Phone video (UGC)" |
| Breathing, blinking, no frozen poses | [../styles/realism.md](../styles/realism.md) motion block |
| Soft front or window light on a face | [../styles/light-direction.md](../styles/light-direction.md) |
| Product in hand | [product.md](product.md) fidelity sentence |

Router shot types ([../model-router.md](../model-router.md)): `avatar-talking-head`, `dialogue-lipsync`, `character-performance`; silent demo shots are `product-motion` or `short-insert`.

Model notes: talking clips with native audio held identity 3/3 and returned the line word for word on Veo 3.1 Fast, audio on, 8 s; Veo 3.1 for a final take [tested] ([../models/veo.md](../models/veo.md)). Silent demo shots went to Seedance 2.0 ([../models/seedance.md](../models/seedance.md)). If the provider has a separate lip-sync or avatar model, check its model file for input order; the prompt rules below still apply.

## Recipe

### 1. Lock the speaker first

Make the identity still (avatar-portrait.md step 5) or a UGC persona still. UGC persona, with the product as image 1:

```
Vertical 9:16 smartphone photo of a real, relatable [AGE RANGE] [LOOK] creator in [SETTING THAT FITS THE AUDIENCE], holding the product from image 1 at chest height, label facing camera, exactly as in image 1: same shape, colors and label. Casual [OUTFIT], natural skin texture, relaxed friendly expression, looking into the lens. Soft window light. No text, no logos other than the product's own label.
```
Make 2 options, pick one, write a one-line casting description (age range, hair, outfit, setting) and paste it into every shot.

### 2. Write one voice block and reuse it

```
Voice block: {voice type}, {accent}, {pace ~2.7 words per second}, {energy}, same mic distance, same voice in every clip
```

### 3. Size the line to the clip

| Clip | Words | Status |
|---|---|---|
| 8 s talking clip | 18 to 22 words fill it | [tested] |
| 8 s talking clip | 13 to 15 words leave 2 to 3 s empty | [tested] |
| Any UGC shot | about 2.5 words per second of shot; shorten if speech sounds rushed | unmarked |

### 4. The talking clip prompt [tested]

```
The same person as the first frame, talking straight to camera, natural confident hand gestures, subtle head movement; {optional one gesture, planned on a gesture not a word}. Head stays level in the same place in frame; hands stay below the chest except that gesture.
Voice: {voice block}.
{The person word} says: {18-22 word line} (no subtitles)
Room tone only, no music, no other voices. Static camera, locked framing, one continuous shot, no cuts.
```

- A gesture lands on its own timing, not on the word you asked for [tested]. Plan any on-screen card on where the gesture lands in the clip.
- Generate all clips back to back from one voice block. The voice still drifted 10 to 13% in pitch between clips in the baseline [tested]; listen and regenerate the outlier (max one).
- Put the spoken line in quotes, with a delivery note: `says, laughing, quick pace: "..."`.
- For a recorded, real feel: SOUND line with small real noises + "No music".

### 5. UGC look

Paste the phone block from motion-shutter.md:
```
Filmed on a phone held in one hand at 30 frames per second in bright daylight, so the phone picks a very fast shutter and the motion is crisp with almost no blur. Slight natural handheld shake, small focus and exposure shifts as [the person] moves, and no cinematic camera moves.
```
UGC tail used on every genre prompt: `Handheld smartphone footage, natural skin texture, slightly uneven home light. No on-screen text, captions, logos or watermarks. Vertical 9:16.`

Slots: `[CREATOR]` = "the creator from image 1, same face, hair and outfit"; `[PRODUCT]` = "the product from image 2, exactly as shown: same shape, colors and label".

### 6. Genre main-shot prompts (UGC)

| Genre | Speaks | Main-shot prompt |
|---|---|---|
| Unboxing | yes | `Close-up of hands opening a shipping box on a kitchen counter, [CREATOR] leans into frame and lifts out [PRODUCT], eyebrows up, says excitedly "[LINE]". Camera handheld at chest height, slight push-in on the product.` |
| GRWM | yes | `Selfie framing from a phone propped on a bathroom sink, [CREATOR] mid-routine, picks up [PRODUCT] and applies it while talking to camera: "[LINE]". Soft window light from the left, relaxed chatty tone.` |
| Problem-solution | yes | `Medium shot, [CREATOR] struggles with [PROBLEM], sighs, then grabs [PRODUCT] and [ONE ACTION THAT SOLVES IT]. Says, relieved, "[LINE]".` |
| Review quote card | yes, third person | `Selfie close-up in a living room, [CREATOR] holds [PRODUCT] at chest height and glances at a phone in the other hand, then talks to camera: "One customer wrote: [EXACT REVIEW LINE]".` |
| Before-after (home only) | optional | `Shot 1: same locked-off framing, [BEFORE STATE]. Cut to shot 2: [CREATOR] uses [PRODUCT]. Cut to shot 3: identical framing, [AFTER STATE], [CREATOR] smiles at the result.` |
| Day in the life | short or none | `Fast montage, [CREATOR]: shot 1 alarm and stretch, shot 2 coffee by the window, shot 3 uses [PRODUCT] at [MOMENT], shot 4 heads out the door. Quick cuts, warm natural light.` |
| 3 reasons | yes | `Medium close-up, [CREATOR] holds up [PRODUCT] and counts on their fingers, energetic: "[REASON ONE]. [REASON TWO]. [REASON THREE]." Jump-cut feel, eye-level phone camera.` |
| Duet reaction (bottom half) | yes | `Close-up, [CREATOR] watches something off-screen just above the lens, jaw drops, then laughs and says "[LINE]", lifts [PRODUCT] into frame.` |
| ASMR demo | no | `Macro close-up, hands slowly [SATISFYING ACTION] with [PRODUCT], shallow depth of field, soft top light, crisp tactile detail, quiet room.` |
| Street interview | yes, two voices | `Handheld street shot, a microphone with a foam cover enters from the right edge, off-camera interviewer asks "[QUESTION]". [CREATOR] on a busy sidewalk, laughs and answers "[LINE]", pulls out [PRODUCT]. Daylight, city noise.` |
| Founder story | yes | `Medium shot in a small workshop or home office, [CREATOR] sits on a stool with [PRODUCT] on the desk, talks warmly to camera: "[LINE]". Slow push-in.` |
| Comparison | yes | `Tabletop medium shot, [CREATOR] behind a table with a plain unbranded [RIVAL TYPE] on the left and [PRODUCT] on the right, tries each, says "[LINE]", pushes [PRODUCT] toward camera.` |
| Hack / tip | yes | `Top-down counter shot, [CREATOR]'s hands show the wrong way, then switch to [PRODUCT] and [HACK ACTION]. Cut to [CREATOR] face to camera: "[LINE]".` |
| POV | short or none | `First-person-feeling shot, [CREATOR] slumped at a desk at [TIME], looks at camera deadpan, then reaches for [PRODUCT] and perks up. Quiet office light.` |
| Trend audio | no (sound added on the platform) | `Quick-cut sequence, [CREATOR]: shot 1 covers the lens with a hand, shot 2 reveals them holding [PRODUCT], shot 3 spins to show [DETAIL], shot 4 confident hero pose. Snappy transitions, bright light.` |

If a beat needs a different framing than the persona still (hands-only close-up, another room), make a keyframe still from the same references first and use it as the first frame.

### 7. Honesty rules for UGC

- The AI creator never claims personal results ("it fixed my skin", "it worked for me").
- No before-after for health, beauty, skincare, hair or fitness results.
- Review lines only from real reviews the user supplies, quoted word for word, read as someone else's words.
- Founder story only with the real story; the persona says "our founder", never a fake named person.
- Tell the user to switch on the platform's AI-content label when posting, where the platform requires it.

### Filled example (talking clip, 8 s)

```
The same person as the first frame, talking straight to camera, natural confident hand gestures, subtle head movement; at about 5 seconds she taps the tablet resting on the counter once. Head stays level in the same place in frame; hands stay below the chest except that gesture.
Voice: warm alto, light Irish accent, about 2.7 words per second, calm and friendly, same mic distance, same voice in every clip.
The woman says: "I used to spend Sunday night building the week's rota by hand. Now I set it once and it just runs." (no subtitles)
Room tone only, no music, no other voices. Static camera, locked framing, one continuous shot, no cuts.
```
(21 words.)

## Pitfalls → fixes

| Pitfall | Fix |
|---|---|
| Line ends early, dead air | 18 to 22 words for 8 s [tested], or end with "then smiles and holds still for a beat" |
| Speech rushed or cut off | About 2.5 words per second of shot; shorten the line and regenerate |
| Voice drifts between clips | Same voice block, back-to-back runs; regenerate the outlier, max one [tested baseline] |
| Gesture on the wrong word | Plan on the gesture's own timing, not the word [tested] |
| Subtitles burned in | "(no subtitles)" after the line; "No on-screen text, captions" in the tail |
| Music or extra voices appear | "Room tone only, no music, no other voices" |
| Camera drifts or cuts | "Static camera, locked framing, one continuous shot, no cuts" |
| Creator changes between shots | Same persona still as image 1 in every shot; casting line pasted word for word |
| Product in hand changes | Product photo as image 2 with "exactly as shown: same shape, colors and label" |
| Looks like a polished ad, not UGC | Phone video block; "slightly uneven home light"; no cinematic moves |

<!-- Sources: cinematic-story-reel references/prompt-guide.md sections 1, 2 and 5 (talking clip, voice block, word counts; tested in an internal test reel); ugc-factory SKILL.md and references/genres.md (adapted from charlesdove977/UGC-Factory, MIT, and higgsfield-ai/skills marketing references, MIT); prompt-styles motion-shutter.md and realism.md (PromptWise free guides, fetched 2026-10-20). -->
