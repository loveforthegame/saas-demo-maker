# MiniMax H3 and Hailuo (MiniMax H3 Max, Hailuo 3, Hailuo 2.3)

**Model facts (at the time of writing; confirm in your provider):**
- MiniMax H3 Max: 480p or 768p; 5 to 15 s; 1:1, 16:9, 9:16, 4:3, 3:4; first + last frame; no
  audio switch. Fast (about 35 s per run in one test) and cheap.
- Hailuo 3: 5 to 15 s; same aspects. References mode (up to 9 images, 3 videos, 3 audio clips)
  or keyframes mode. Also video to video. Mid cost.
- MiniMax H3 is also released as open weights. A hosted version may add a prompt rewriter, so
  treat the field notes below as strong priors, not guarantees. Hailuo shares the family but the
  field notes were measured on H3.

Check the provider's model options for the exact parameter names (duration, resolution, first/last
frame, reference slots, dialogue tags, audio reference).

## When to pick it

- **Use for:** one-beat acting shots (a breath, a smirk, a wink), performance with body language,
  fast cheap retakes, testing shot structure before a costlier model, audio-reference-driven mouth
  rhythm (Hailuo 3).
- **Not for:** impacts and contact physics, liquids, crowds by count, on-screen text, many beats
  per shot.

## Compile

- **Decide in this order:** purpose (feeling) -> framing -> content (Field notes 0).
- **Slot order:** framing in one line -> subject -> body-first performance with timed beats ->
  light. Describe what is in the frame in detail; how it is shot in one line.
- **Length:** 40 to 120 words.
- **Timing:** `At 0-1.5s [beat]. At 1.5-3s [beat].` One shot holds 1 to 2 expression beats; more,
  split into shots (Field notes 1). Leave about 1.5 s tail; the final second can break.
- **Emotion:** body order, not labels: "lower lids push up first, then the mouth corners lift"
  (real smile), never "he smiles warmly" (Field notes 14).
- **Stillness:** objects as positive states; people as small living actions; camera in ONE
  sentence. Never "nothing changes" or a list of "no zoom, no push-in" (Field notes 2).
- **Size:** crop language ("the top of his head is one hand's width below the frame edge"), not
  fractions or units (Field notes 5). Face beats need the face at least 1/3 of frame height.
- **Impacts:** skip the contact moment; show before and after, put the hit in the sound or edit.
- **Camera commands (Hailuo legacy syntax, may help):** `[Push in]`, `[Static shot]`,
  `[Tracking shot]`, at most 3 in one bracket. The prose must still state the move.
- **References:** shape, headcount and crowd layout come from images, not text (Field notes 6, 10).
- **Audio:** an audio reference (Hailuo 3) drives lip shape and breathing rhythm, not the voice
  itself. Silence must be stated, or the model adds a track.
- **When a reference carries it:** with a first frame or scene image, describe only performance
  and what changes; the scene image locks where the camera stands left to right.

```
[Shot size], [camera height], [static on a tripod | one move]. [Subject trait line, as visible].
At 0-1.5s [body beat]. At 1.5-3s [the one face beat, written as muscle order]. Between beats he
breathes, blinks, weight settles. [Light sources]. [Look line].
```

### Example

Bad (adjectives, many beats, "nothing moves"):
> The boxer looks down amused, smirks, laughs, then gets serious, then winks. Nothing else moves,
> no zoom, no pan, no push-in.

Good (first frame given):
> Close-up, camera slightly below his chin, static on a tripod. The giant boxer with the thick
> black beard looks down at the boy below frame. At 0.5s his head tilts a few degrees down. At
> 1.2s his lower lids push up first, then one corner of his mouth lifts into a slow smirk that
> holds. Between beats he breathes and blinks; sweat beads on his forehead catch the ring lights.
> Warm tungsten backlight.

## Self-check

- [ ] Intent -> framing chosen on purpose (not centred eye-level by default)
- [ ] 2 or fewer expression beats; emotions written as body order
- [ ] Camera in one sentence; no "nothing changes"
- [ ] No impact or liquid volume on screen
- [ ] About 1.5 s tail left at the end

## Failure modes

| Problem | Fix |
|---|---|
| Frozen face | too many beats; one beat per shot, fill time with countable small events |
| Face morphs like rubber | hide the change behind a blink or head dip; counter-beat first |
| Character looks into the lens | move the camera to where they look; "does not look into the lens" |
| Hand-object contact fails | make the moving body part the subject; contact from frame 1 |
| Crowd count wrong | set it in the scene image, not text |
| Cut lands late | tie it to an event, not a timestamp |
| Two people from two refs of one person | headcount block (Field notes 6) |
| Mascot or product gets stained | cut the contact preposition (Field notes 7) |
| Dialogue restarts or repeats | remove continuation words; fill time after the line with action (Field notes 17) |
| Last second breaks into noise | 1.3 to 1.5 s slack at the end |

## Field notes

Distilled from a production diary of an episodic series shot on MiniMax H3. Every rule was
observed on real renders.

### 0. Decide in this order: purpose, framing, then content

1. What must the viewer feel from this shot? Write it as a feeling ("this is the high point of
   his life"), not an action.
2. What framing delivers that? Camera height, shot size, where the person sits in frame,
   foreground, eyeline. Low angle = dominant. High angle = pressed down. Centred = neutral.
   Off-centre with lead room = going somewhere. People in foreground = surrounded. Empty
   background = alone.
3. Only then write performance, light, dialogue, props.

Neutral framing (centred, eye level, frontal) is what you get when framing is an afterthought; it
reads as an interview or ID photo. Review a take by asking "did it achieve its purpose" before
"did it match the shot list".

### 1. One shot cannot hold many beats

Pack many facial beats into one shot and the model averages them into nothing. Measured: a 7 s
close-up with 9 beats had a frozen face; the same beats split into three 2 to 3 s shots, one main
beat each, all landed.

- Count beats. More than 2 or 3 expression beats in a shot: split it.
- Cuts are performance: the audience re-reads a character at every cut.
- Shots with a spoken line get more screen time from the model; it steals time from other shots
  in the same run. Shots that must keep background continuity should not share a run with a
  dialogue shot.
- A silent character can still act. Big body moves are safer than face beats:

| Face (riskier) | Body (stable) |
|---|---|
| jaw clenches once | long breath out through the nose, shoulders drop |
| blink, eyes fall to the floor | hand wipes down the trouser leg, grabs the back of the neck, head drops |
| upper lids fly open | head pulls back a few centimetres |
| lower lip tucks in | the held object loosens and tilts down |

Locomotion (sit up, stand, walk to a spot) almost never fails.

### 2. Never write "nothing changes"

"Nothing about her changes: her eyes stay, her mouth stays, her head does not move" leaks into the
whole shot and freezes what should move. A pause belongs in the edit: end shot A on the stopped
action, start shot B on the reaction.

Three kinds of stillness, three rules:
- Objects: write it as a positive state. "The pen stays in contact with the desk; the gap between
  pen and folder is the same in every frame."
- People: write the small things they do instead (breathing, blinking, weight settling).
- Camera: one sentence only: "static, on a tripod, with no camera movement whatsoever." Adding
  "no push-in, no zoom, no dissolve, no intermediate framing" made the cut drift later, twice.
  Removing them fixed it.

### 3. Don't film impacts or liquid volume

The model cannot do contact-driven cause and effect or hold a liquid volume. Asked for "hand
knocks over cup, coffee floods the desk": the hand never touched the cup, the cup fell by itself,
more coffee than a cup holds, hard sticker-like edges, still flowing after it stopped.

- Skip the moment. Shot 1: an arm sweeps past the lens until it fills the frame. Shot 2: it has
  already happened, the cup lies on its side, the spill has stopped. Put the crash in the sound.
  The sweep is a natural cut and is locomotion, the most reliable class.
- Fix liquid with a boundary: "spread about as far as the width of a hand and no further".
  Words like "widening", "spreading" have no end, so it keeps growing.

### 4. Make the moving body part the subject

"The hand takes the cover and swings it over" renders the cover moving by itself, hand along for
the ride.
- Declare it: "in this shot what moves is the hand; the folder is only what the hand carries".
- Write the joint path: wrist turns, knuckles lift over the fold, forearm rolls, fingertips land
  last.
- Add zero distance: "the palm stays in contact with the card from 0.8 s to 2.0 s".
- Add the counterexample: "there is no frame where the cover moves and the hand does not".
- The hand should already touch the prop in the first frame, not enter from off-screen.
- Two hands are more stable than one if their jobs are split (one holds down, one closes).

General: "A carries B" is written as A's joints moving plus A-to-B distance fixed at zero.

### 5. Size: describe crops, not fractions

"About two thirds of the frame tall" rendered at 45 to 52 %. Crop language got 69 % in one go:
- "the tips of its ears are one hand's width below the top edge"
- "its base spills past both the left and right edges"
- "the bottom edge of the frame cuts across just below the front of the base"
- "it is by far the largest thing in the picture"

Other rules:
- Limit a secondary object by what enters frame ("only fingers and the front of the palm are in
  frame") instead of giving its size.
- In 9:16, a subject about as wide as tall, shown whole, tops out near 50 to 60 % of frame
  height. That is geometry. To go bigger, crop it (usually the bottom).
- Distances with units are ignored too. Use objects in frame as rulers: "between the pool and its
  base is a band of dry wood as wide as the figurine is tall".
- Overhead views flatten characters and break relative scale. Put the camera at table height
  looking across.
- Write size three ways: compared to a known object, absolute size, and frame crop. The first two
  get physics right; only the crop makes it look big.

### 6. Shape and headcount come from images

- Text failed three times to get a 1.75:1 panel (got a square). One reference image fixed it. For
  screens, boards, cards: feed a blank version with the right shape and glow, composite content
  later. Never feed a reference full of symbols or UI text: they come out garbled.
- Two reference photos of one person (front + three quarter) in a moving shot produced two
  people. Add a headcount block: "there are exactly two people in this room, A and B, nobody
  else; picture 3 and picture 4 are the same man from two angles, one person, never two." Empty
  chairs and spare faces become candidate people.
- Crowd size and layout are set by the scene image, not by text. Numbers, head counts, area and
  geometry all failed (asked 15, got 20 to 30). A scene image with the crowd already placed worked
  first try, and the prompt shrank from 16,000 to 6,900 characters. Text says what they do (clap,
  raise glasses) and what must not change (same count, nobody sits).
- Feed a character's reference to the step that decides they exist. If the scene image puts
  people in the room, make that image with the character references, not the video.

### 7. Brand characters stay clean

"Coffee glistening around its base, the light through the wet film" made the mascot cry mud. Any
preposition that links a staining thing to a surface that must stay clean (on, around, through,
soaks into, film) gets painted, and over-painted. Keep the tension, cut the contact: "a dark pool
lies on the wood a hand's width behind it, holding the amber light as a long reflection; its
cream-white surface is dry and matte all over."

### 8. Performance needs screen area

Unexecuted beats, flattened physique and a busy frame usually have one cause: the camera is too
far. Same shot, same text, only shot size changed: heads at 1/7 of frame height lost the beats and
the build; heads at 1/3 performed them.

- Physique or distinctive features need size. In wides, separate people by silhouette and
  position.
- Emotional landings always get a close shot.
- Wides carry big body moves only (clap, raise a glass), never face beats.
- Framing is set by what must fit in the frame, not by adjectives. List what must be visible; the
  lowest item sets the loosest possible framing. Want closer: move items to another shot or state
  they are out of frame. Every connected reference image counts as "must be visible".
- Small distant faces blur at a system level; no prompt, steps or resolution fixes it. Wides are
  for space, not identity.
- In wides bind identity to screen position, not names: "the one on the left is short and broad,
  the one on the right is tall and narrow, a full head taller; the raised arm with the bottle
  belongs to the one on the left, and there is exactly one raised arm."
- Anchors by reliability: left/right position, silhouette, garment category (not colour), then
  one countable constraint.

### 9. Camera placement before expression

When what a character looks at is off-frame, the model makes them look at the lens.
- Looking down at something small: put the camera at table height beside it, looking up. Looking
  down now faces the lens.
- Talking to someone crouched: camera low at the crouched person's position.
- Watching a side TV: camera next to the TV (the interview setup).
- When the pose is locked by the story, move the camera, not the character. Then state "does not
  look into the lens".
- What a character looks at cannot also be behind them. A crowd cheering for him belongs on the
  camera side, living in the sound. Establish a crowd once; after that it can live in the audio.

### 10. What a scene image locks

A scene reference locks where the camera stands left to right, not how high. Raising the camera
above heads worked from text (tilt came out lighter than asked); moving it to a corner or diagonal
did not. To change side or axis, make a new scene image. Raising the camera is the cheapest fix
for foreground heads blocking the subject.

### 11. The same person across shots

Every shot rebuilds the person from text. "Same woman", "same outfit as shot 1" supply nothing.
Paste 6 to 8 concrete traits (eye colour, hair colour + length + style, marks, glasses, earrings,
the garment and its colour) into every shot, word for word. Paraphrase re-rolls the face. Same for
voice: one concrete voice line copied every time.

### 12. Don't name what shouldn't appear

Mentioned objects tend to appear: "proportions of a phone screen" can grow a phone. Frame the
shape with frame edges or a reference image. Exception: silence in the audio must be stated, or
the model adds a track.

Universal rules reach further than intended: "every person in the room turns toward the focal
point" also turned the hero standing on the focal point. Narrow the scope ("everyone in the
horseshoe, meaning all but those two") and add the positive exception. A positive rule is executed
faithfully even when wrong: "cars evenly spaced" made a pattern, not traffic. Write "traffic is
bunched, three or four nearly nose to tail, then long gaps; lanes out of sync" separately from
"nobody brakes hard or cuts in". After every suppressing rule ask: what else does this block?

### 13. Edit the whole prompt, not one line

Prompts grow by accretion and the model executes every sentence, including the old ones. Before
changing any spec, search the whole prompt for every phrasing of it:
- hands: hand, arm, shoulder, hold, touch
- position: left, right, behind, in front
- facing: face, turn, toward, look
- framing: frame, edge, above, below
- timing: every "from X to Y seconds" once you add or move a shot

Summaries and shared blocks count as much as the main text. When the framing changes, re-read
every sentence: a harmless line for a tight frame comes alive in a looser one.

### 14. Emotion has a body order

- Real smile: eyes first (lower lids push up, crow's feet), mouth follows. Mouth-only is the
  social fake smile.
- Relief: brow releases, breath out, shoulders drop, eyes focus, mouth corners lift.
- Suppression: brow and eyes leak, mouth holds; delay the mouth 0.3 to 0.5 s.
- Micro-expression order: brows (first, smallest), eyes, mouth (last).

| Emotion | Don't write | Write |
|---|---|---|
| confused | confused | inner brows draw together and down, head tilts about ten degrees, eyes flick between two points once |
| uneasy | uneasy | slower heavier blinks, one swallow, shoulders rise a centimetre and settle |
| shocked | shocked | head pulls back, upper lids fully open, inhale holds the shoulders high |
| holding back tears | holding back tears | lower lip tucks in, faster blinks, eyes drift up away from the other face |
| relieved | relieved | shoulders drop once, held breath escapes from the corner of the mouth |
| irritated | irritated | breath out through the nose, shoulders drop, palm wipes the trouser leg, grabs the back of the neck |

Breath is the base beat; a held breath (shoulders parked high) reads as tension and is easy for
the model. Hands are honest but write contact and motion, not finger shapes.

### 15. Transitions: hide the change

Writing "the crease between her brows smooths out" gives a start and end state and the model
cross-fades: the face morphs like rubber.
1. Hide it behind cover: eyes close and head dips, the brow releases while the eyes are shut,
   then (or after a cut) the eyes open onto a face already loose. This even swaps a design look
   (eye style) inside one shot if the cover is long enough. Describe closed eyes by shape ("each
   eye a single smooth curved line") so a half-lidded reference doesn't pull it.
2. Counter-beat first: tighten before release, hold before tears. A change with no resistance
   looks like a switch.
3. Put the trigger in the same or adjacent shot, with a beat to receive it.

### 16. Amplitude adds up; fill time with events

- Components add. "Bigger, funnier" written as five smile components read as flippant.
  Restraint = one component + a list of parts that must not move ("cheeks don't lift, eyes don't
  narrow, brows don't rise, head doesn't tilt back; only the mouth betrays him"), and state the
  size holds without spreading.
- Write "take it back" as a motivated action (he's called back into the room: head returns, eyes
  return, mouth goes level), leave at least 1.5 s after it, and say "the last frame's face matches
  the first frame after the cut".
- Background life: "between beats he is alive: breathing, small eye movements, weight settling;
  blinks at 2.4 s and 5.0 s; no frame is frozen." Put this before the big beats.
- Time with nothing in it gets squeezed out. To hold a face 3 s, fill it with countable events
  (mouth settles, blink, eyes drop to the prop, breath, eyes return, blink).
- A face reads in 1.5 to 2 s. More is dead frames.

### 17. Dialogue failures (false starts, repeats)

Causes found by word-timestamp transcripts:
1. The prompt implies he is mid-speech ("continuing", a line starting with "And"). Remove
   continuation words.
2. Speed written two ways in different blocks (brisk here, unhurried there). Make them one.
3. No "say it once". Adding "he says these two sentences once, at one even speed; he does not
   restart, repeat or stumble" helped, but that sentence itself was sometimes spoken aloud.
   Better: fill the time after the line with an action ("he waits, turns a page; silence is the
   rest of the shot").
4. Speech rhythm follows the take, not the prompt: the same take with different prompts gave
   identical word timings. Bad audio: re-run a new take before rewriting. Run 2 or 3 takes for
   dialogue shots and keep the clean one.
5. Any sentence about speaking gets spoken. In dialogue shots avoid say / sentence / word / line
   outside the dialogue itself. "Lips part as if to speak" made him speak. Silence is written as
   a closed-mouth action.

- If the voice will be replaced by a real recording, line length is a hard limit: characters /
  speaker rate = seconds needed. Lip-synced lines only; voiceover shots are cut to picture.
- Put beats that follow the line in the next shot; the model treats the whole shot as speaking
  time.
- Emotion goes in delivery description, not inside the spoken text.

### 18. Cuts and camera moves inside one run

- State the cut structure as countable facts: "this clip has exactly two cuts, at 4.9 s and
  9.2 s, no others. The camera never returns to a shot it has left. The last frame is A's face."
  Make the shot that must hold the longest.
- Camera motion is global. Want cuts: keep everything static. Want a move: no cuts inside.
  Exception: cuts between very different subjects and sizes (tabletop insert to a face) hold.
- Cuts drift later (measured +1.2 s) while beats inside a shot stay relatively accurate. Tie a
  flash or hit to an event ("the moment the card stops beside her face"), not a timestamp. Make
  lead-in shots longer than needed and check how much time is left after the real cut.
- Reverse angles need a lead-in: a 1.5 s two-shot before the single gives the model the geometry.
  Also works to reach an angle the scene image doesn't show: shot 1 matches the scene image's own
  view, then cut. Trim the lead-in in the edit.
- For several shots from one angle, grab a clean frame from an accepted take (mouth closed, no
  blur, default pose) as the composition anchor for all of them, instead of re-deriving each. Say
  it sets camera, framing, room and light, not pose or expression. Don't chain last frames:
  quality drops each hop.
- To turn the camera 90 degrees, write consequences: "he is no longer in profile; he faces the
  lens, shoulders square; the desk now runs toward camera; a different wall is behind him." Add a
  wrong-side detector: "if any part of the whiteboard is visible, the camera is on the wrong side."
- POV without your own body: make the frame's bottom edge a physical thing ("the bottom of the
  frame is the near edge of the desk; his hands rest on his knees below it").
- One-take or POV requests: any second shot is a defect. Write exactly one shot, with start, path
  and end of the move.
- Exposure jumps across cuts in the same run and text can't fix it. Grade per shot in the edit.
- Same take, same structure: cuts land on the same frame, so two versions can be spliced at the
  cut. Don't chase every segment landing in one run.

### 19. Length and tails

- Renders can break into noise in the final second or so. Check the last frames of every clip.
- More cuts, more tail risk. Emotional scenes trade cuts for performance; empty and transition
  shots stay single.
- "Longest we ran" is not "the limit". A 15 s run succeeded after 8.7 s had been written down as
  a ceiling.
- Test structure at low resolution and the shortest duration first (shot structure, rhythm, audio
  present), then step up.
- Ask first whether a shot needs a run at all: a repeated line, a reaction, an insert can often be
  trimmed from an existing take.

### 20. Verify with numbers, fix the last mile in the edit

- Did an expression happen: grab a frame before and after the beat,
  `ffmpeg -i a.png -i b.png -lavfi "[0:v][1:v]psnr" -f null -`. Over 45 dB frozen, 30 to 40
  breathing only (fail where emotion was due), 18 to 28 clear action, under 15 a cut.
- Stills judge framing, who is present, wardrobe, set, light direction. They cannot judge
  actions, intent or rhythm; watch the clip.
- Late reaction: cut the dead time and cover with an insert of the trigger; come back already
  reacting. Too-smooth change: bring the two ends close with a short insert between. Recut before
  re-prompting.
- Never ask the model for screen content, logos, precise text or held freezes. Screens get "even
  cool white light"; content, text and holds go in during editing.
- An audio reference can drive lip shape and breathing rhythm but does not reproduce the voice
  (pitch, range, accent drift). Treat it as a performance scaffold; the final voice is a real
  recording.

Sources: production diary of an episodic series on MiniMax H3 (internal field notes); Akool Hailuo
guide (failure modes); Hailuo bracket camera commands (third-party).
