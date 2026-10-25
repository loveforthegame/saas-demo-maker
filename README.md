# SaaS demo maker

Short, story-led product ads (8 / 15 / 20 s) for any SaaS or app. Claude asks about your product, pitches 3
concepts, shows a storyboard table for your yes, then generates stills and video through the Predis MCP and
builds the film in HyperFrames.

## Install

In Claude Code:

```
/plugin marketplace add loveforthegame/saas-demo-maker
/plugin install saas-demo-maker@saas-demo-maker
```

On Claude Code 2.1.275 or later, one line works: `/plugin install saas-demo-maker --marketplace loveforthegame/saas-demo-maker`

## Use

In Claude Code: `make an 8 second demo ad for <product, URL>` (or `/saas-demo-maker:saas-demo-maker`).

## Needs

1. **Predis MCP connector** (generation engine) connected in Claude, on a paid plan with credits.
   An 8 s ad costs about 330 credits per round.
2. **HyperFrames skills:** `npx skills add heygen-com/hyperframes --all`
3. **Node.js 18+, ffmpeg, Python with `openai-whisper`** (`pip install openai-whisper`).

Bundled: `saas-demo-maker`, `predis-director`, `prompt-styles`, a Mixkit SFX kit and the Inter font.
