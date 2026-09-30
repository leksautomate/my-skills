# my-skills

My personal agent skills (prompts only).

## almighty-ugc-factory/

ONE self-contained folder — copy it anywhere, use it with any AI.
The top-level `SKILL.md` inside is the master: it asks whether you
want a talking-head script or a multi-shot video with camera
direction, then routes to the matching sub-skill, both nested inside
the same folder:

```
almighty-ugc-factory/
  SKILL.md                     <- master router (start here)
  ai-ugc-video-production/     <- Route A: talking-head scripts
  ugc-content-factory/         <- Route B: multi-shot director-first prompts
```

Route A material from [agent-media-skill](https://github.com/yuvalsuede/agent-media-skill);
Route B material from [ugc-factory-skill](https://github.com/TheMattBerman/ugc-factory-skill).
Prompts only: no generation, no API keys, no credits.
