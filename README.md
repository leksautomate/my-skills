# my-skills

My personal agent skills (prompts only).

## Almighty UGC Factory

A three-skill UGC prompt system. Start with the master — it asks whether
you want a talking-head script or a multi-shot video with camera
direction, then routes to the matching sub-skill.

| Folder | Skill | What it does |
|---|---|---|
| `almighty-ugc-factory/` | **Master (start here)** | Routes every UGC request: asks "talking-head script or multi-shot video with camera direction?" |
| `ai-ugc-video-production/` | Route A — talking-head | Script templates, product-acting scenarios, subtitle styles, word-count rules (from [agent-media-skill](https://github.com/yuvalsuede/agent-media-skill)) |
| `ugc-content-factory/` | Route B — multi-shot | Director-first UGC: creative brief → visual beat sheet → synchronized script → assembled Kling video prompts (from [ugc-factory-skill](https://github.com/TheMattBerman/ugc-factory-skill)) |

All skills are prompts-only: no video/image generation, no API keys,
no credits.
