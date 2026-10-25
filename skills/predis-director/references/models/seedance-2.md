# Seedance 2.x (`seedance_2_0`, `seedance_2_0_fast`, `seedance_2_5`)

**Predis options:**
- `seedance_2_0`: `resolution` 480p|720p|1080p|4K (default 720p), `duration` int 4-15 + auto,
  `aspect` 1:1|16:9|9:16|4:3|3:4, `audio` (default true). 12 cr/s at 720p, 30 cr/s at 1080p.
- `seedance_2_0_fast`: 480p|720p only, otherwise the same. 10 cr/s.
- `seedance_2_5`: 480p|720p|1080p, `draft` bool, `duration` 4-30 + auto, aspect adds `adaptive`,
  audio. 19 cr/s at 720p.
- Ref modes: `references` = images (9; 2.5: 30) + videos (3; 2.5: 10) + audio (3; 2.5: 10), audio
  cannot be the only ref. `keyframes` = first_frame + last_frame + video/audio refs. Video/audio
  refs 2-15 s each, 15 s total (2.5: 30 s). A video ref locks aspect to adaptive (2.5).
- `content_agreement: true`: realistic human faces in refs may be refused by the provider.
  Use generated faces, not photos of real people.

**Use for:** multi-shot sequences in one clip, crowds and ensembles, reference-heavy scenes
(identity + motion video + music), long clips on 2.5.
**Not for:** a single 2 s insert (4 s minimum), photo refs of real people.

## Compile

Order: **reference roles -> subject + action -> scene -> camera -> light/style -> audio ->
constraints**. Length 40 to 110 words per shot. Chronological.

```
@Image1 (image 1) is the first frame. @Image2 (image 2) sets the boy's face and outfit only.
[Subject] [action with endpoint]. [Scene only if refs do not show it].
Camera: [one move with endpoint]. Light: [source]. [look_line].
Sound: [specific sounds tied to actions]   <- only if audio on
```

- Reference tags: `@Image1..`, `@Video1..`, `@Audio1..` numbered per type in upload order. Write
  the tag with its job every time ("follow @Video1 for camera movement only"). Keep a plain-word
  echo "(image 1)" so the sentence still reads if the host maps references itself.
- Multi-shot: label every cut `Shot 1:` `Shot 2:` ... with ~4-6 s each (3 shots = 12-15 s). Per
  shot: one action, one move, its sound. End each shot on the completed beat. Persistent look
  declared once: "warm tungsten haze throughout, every shot". One take: "single continuous take,
  no cuts".
- i2v hold mode (the image is the moment): 3-4 micro-actions + a positive-plus-negative pose lock
  ("he stays seated; he does not stand"). React mode: give the key beat >= 2 s.
- Audio refs: "@Audio1 sets tempo only". Dialogue in quotes in the shot where the speaker is on
  screen; lock framing for lip-sync.
- Fast tier honours multi-shot, slow motion and dolly moves less reliably: draft on fast, final on
  `seedance_2_0`.

## Good vs bad

Bad (one ref doing four jobs, no labels):
> Use this image, kids cheering in the gym, then they jump, cinematic, dynamic, epic energy.

Good (keyframes, first_frame = B4):
> @Image1 (image 1) is the first frame. About twenty schoolkids in matching yellow t-shirts press
> against the red ropes and scream, fists pumping; the girl in front pumps her hand-drawn
> cardboard sign "GO LEO!" up and down three times. Camera: kids' eye level, handheld, slow drift
> left along the ropes. Warm tungsten overheads, dust in the beams. 35mm film, soft grain.

## Failure modes

| Symptom | Fix |
|---|---|
| Request refused | refs contain realistic real-person photos -> use generated stills |
| Long prompt renders as one take | label shots |
| Look flickers between shots | same look phrase every shot, or "throughout" once |
| Ref fights the prompt | delete re-description; add what does not transfer |
| Product/logo warps | "static identity, no shape change"; give it its own shot |
| 1080p bill shock | draft 720p; 1080p only for the final |

## Self-check
- [ ] Every tag has a stated job; tag numbering = reference_ids order per type
- [ ] 40-110 words per shot; shots labelled if > 1
- [ ] Duration fits shots x 4-6 s; >= 4
- [ ] Resolution chosen on purpose (720p unless final)

Sources: RunDiffusion Seedance 2.0 guide (modes, @image1 roles, limits, face restriction),
Magichour reference guide, predis-prompting/references/seedance.md.
