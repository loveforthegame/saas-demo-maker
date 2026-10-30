# Working from an existing clip: restyle, edit, motion transfer, extend

Models (at the time of writing; confirm in your provider):

| Job | Model | Notes | Cost |
|---|---|---|---|
| Restyle / edit, final | Runway Aleph 2 | source video + up to 4 images; picks its own length | premium |
| Restyle / edit, cheap test | Wan 2.7 video edit | 720p or 1080p; 2 to 10 s; aspect auto, 16:9, 9:16, 1:1, 4:3, 3:4; 1 video + 1 image | cheap |
| Edit with character or object refs | Kling 3 Omni | up to 7 images + 1 video (see kling.md) | premium |
| Cheap simple edits, extensions | Gemini Omni Flash | see gemini-omni.md | cheap |
| Video edit mode | Seedance 2.0 / 2.5 | "video 1 is the source; change only X" (see seedance.md) | mid |
| Motion transfer | DreamActor M2 | 1 character image + 1 driving video; picks its own length | cheap |
| Extend | Grok Video Extension | source clip; 2 to 10 s added (see grok-video.md) | cheap |

How each provider takes the source clip, the maximum input length, and whether source audio is
kept: check the provider's model options.

## When to pick it

- **Use for:** restyle, relight, weather or time-of-day change, add / remove / replace an object,
  wardrobe swap (Aleph for the final, Wan video edit to test the idea); a still character
  performing a driving video (DreamActor); continuing an accepted clip (extension).
- **Not for:** changing the framing or camera angle from text alone (give a still of the target
  framing instead), or many changes in one pass.

## Compile (edit and restyle models)

- **Slot order:** source statement -> one change (action verb: add, remove, replace, restyle,
  relight) -> keep line.
- **Length:** 10 to 40 words. Short and direct beats long and descriptive; long edit prompts cause
  unintended changes.
- **Timing:** none; the clip already carries composition, motion and timing.
- **References:** the source video is video 1. A style image: "image 1 sets colour palette and
  texture only; people and layout come from the video."
- **Audio:** strip the source audio first if you want new sound (see Prep).
- **When a reference carries it:** never re-describe what the clip shows. Name only the change.
- **One layer per pass:** look, then weather, then an added object. Stack passes instead of one
  big ask.

```
Video 1 is the source. [Verb] [exact target] [to what]. Keep the framing, people, motion and
timing the same.
```

### Example

Bad: `Make the video better, more cinematic and moody with rain and also anime style and a cat.`
Good: `Video 1 is the source. Relight the scene as late night with wet sodium-orange streetlight
from frame right. Keep the framing, people, motion and timing the same.`

### Edit recipes

| Want | Prompt |
|---|---|
| Style | "Make this video hand-drawn anime, cel shading, bold outlines. Keep everything else the same." |
| Time / weather | "Make it night with heavy rain and wet reflections. Keep the people and camera move the same." |
| Wardrobe | "Put the man in a navy tailored suit. Keep his face and movement the same." |
| Add object | "Add a small black cat that jumps onto his lap; he pets it. Keep everything else the same." |
| Remove object | "Make the phone in her hand invisible. Keep everything else the same." |
| Change sign text | `Change the sign to say "OPEN LATE". Keep everything else the same.` |
| Relight | "Relight with a warm key from frame left and a cool rim from behind." |

## Compile (motion transfer: DreamActor M2)

- The work is in the inputs. One character image gives identity; one driving video gives motion.
- Driving video: one performer, one clear action, clean silhouette, steady camera. Busy
  multi-person footage transfers noise.
- Character image framed like the driver (both full length, or both waist up), clear limbs,
  plain background, one person; similar aspect ratio for image and video. (Common-sense checks,
  not documented by the model maker.)
- Prompt, if the model accepts one: identity locks only: "keep the character's face, outfit and
  colours exactly as the image".
- Transfers well: choreography, gesture timing, blocking. Transfers poorly: fine hand detail,
  multi-person sync, subtle facial acting.
- Use owned, licensed or self-recorded driving footage. Only the motion should carry over, never
  the performer's likeness.
- Reference-based alternative on Seedance 2.x: one donor video + one identity image with "the
  video controls the choreography only; nothing of its performer, costume, room or logo
  transfers" (see seedance.md).

## Compile (extend)

- Source is the accepted clip. Prompt only what happens next, starting from the observed last
  frame: "Continue: she reaches the door, pauses, pushes it open into bright daylight. Camera
  keeps its slow follow."
- Carry over the direction and speed of subject and camera; a motion that was mid-way must keep
  going.
- Don't replay beats that already happened and don't leak the ending planned for a later part.
- Each hop adds drift. After a few extensions (2 hops is a safe limit), re-anchor: make a new shot
  from the original reference image instead of extending again.
- Want a new angle rather than a continuation: a new shot (image to video from a frame or the
  original reference), then cut.

## Self-check

- [ ] Exactly one change + a keep line
- [ ] Source trimmed to the model's limit; audio stripped if new sound is wanted
- [ ] Motion transfer: single performer, framing of image matches the driver
- [ ] Extension starts from the observed last frame, not the planned ending

## Failure modes

| Problem | Fix |
|---|---|
| Unintended changes | shorter prompt, one change, keep line |
| Framing ignored | give an image of the target frame |
| Transfer has two people or noise | single-performer driver, matching framing |
| Extension drifts | shorter hops; re-anchor on the original reference |
| Restyle looks messy | cleaner source: steady camera, one clear subject, no burned-in captions |

## Field notes

### Prep the source (always)

```bash
ffprobe -v error -show_entries format=duration,size:stream=width,height,r_frame_rate -of json in.mp4
ffmpeg -i in.mp4 -ss 0 -t 10 -vf "scale=-2:720" -c:a copy prep.mp4      # trim + downscale
ffmpeg -i in.mp4 -an -c:v copy silent.mp4                               # strip audio for new sound
```

Trim to the model's maximum duration before upload. Upload size limits exist on most providers
(200 MB was the cap in one setup). Clean inputs restyle best: steady camera, one clear subject,
no burned-in captions.

Source-first wording that works: "Video 1 is the source clip; preserve composition and timing;
change only the lighting to late-evening sodium streetlight."

Grab the last frame to check extension continuity:
`ffmpeg -sseof -0.1 -i clip.mp4 -frames:v 1 last.jpg`

Sources: Runway Help Center Aleph article (via summaries); Runware Aleph 2.0 editing guide;
DataCamp Aleph test; internal production field notes.
