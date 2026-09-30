---
name: "almighty-ugc-factory"
description: "Almighty UGC Factory — MASTER UGC skill (PROMPTS ONLY). Single self-contained entry point for ALL UGC prompt and script requests. First ASK the user: talking-head script, or multi-shot video with camera direction? Then route to the matching sub-skill INSIDE this folder: talking-head → ai-ugc-video-production/SKILL.md; multi-shot → ugc-content-factory/SKILL.md. Trigger on 'UGC', 'Almighty UGC Factory', 'UGC ad', 'UGC video', 'UGC prompt', 'UGC script', 'make a UGC', or any request to create UGC content."
metadata: { "includeInPrompt": true }
---

# Almighty UGC Factory — Master Skill (Prompts Only, Self-Contained)

## Purpose
One folder, one entry point for all UGC work. This folder contains
everything — no external files or workspace paths are needed:

```
almighty-ugc-factory/
  SKILL.md                      <- this master router (start here)
  ai-ugc-video-production/      <- Route A sub-skill (talking-head)
    SKILL.md
    references/prompts.md
  ugc-content-factory/          <- Route B sub-skill (multi-shot)
    SKILL.md
    references/ (Modules A/B/C, prompt assembly, characters, settings)
```

All paths in this skill are RELATIVE to this folder, so it works on any
machine, with any AI assistant: copy the whole folder, point the AI at
this SKILL.md, and everything it needs is inside.

Everything is PROMPTS ONLY: no video/image generation, no CLI, no API,
no login, no credits, on either route.

## Step 1 — ASK FIRST (routing question)

On any UGC request where the user has NOT already made the style clear,
ask before doing any work:

> "Do you want a **talking-head script** (one creator talking to camera,
> quick and simple), or a **multi-shot video with camera direction**
> (director-first: brief, beat sheet, script fitted to shots, assembled
> video prompts)?"

In chat, present this as a two-option tap choice when an options widget
is available ("Talking-head script" / "Multi-shot video with camera
direction").

Skip the question and route directly when the request already implies a
route, for example:
- "Kling prompt", "beat sheet", "director-first", "multi-shot",
  "camera direction", "ugc factory" → Route B
- "SaaS review script", "product acting", "show your app",
  "subtitle style", "quick script", "talking head" → Route A

If the user wants both, run Route A first, then Route B.

## Step 2 — ROUTE

### Route A — Talking-head script
Sub-skill (in this folder): `ai-ugc-video-production/SKILL.md`
Read it, plus `ai-ugc-video-production/references/prompts.md`, then
follow that sub-skill's workflow and output contract exactly:
script templates (monologue, testimonial, product-review,
problem-solution, saas-review, before-after, listicle, product-demo),
2.5 words/sec word-count rule, product-acting scenarios, subtitle styles.
Deliverable: the finished prompt/script text, ready to paste.

### Route B — Multi-shot video with camera direction
Sub-skill (in this folder): `ugc-content-factory/SKILL.md`
Read it, plus its references under `ugc-content-factory/references/`
(Modules A/B/C, Module D prompt assembly, character library, scene
settings), then follow that sub-skill's pipeline exactly:
Creative Brief → Visual Beat Sheet → Synchronized Script → assembled
per-shot video prompts / multi_prompt JSON. Keep its approval gates
unless the user asks for a full one-shot run.

## Operating Rules
1. Never do UGC work "freehand" when a request matches this master —
   always route through one of the two sub-skills in this folder.
2. Do not copy sub-skill content into this file; if a sub-skill's
   instructions and this file ever conflict, the sub-skill wins for its
   own route.
3. Only use files inside this folder. If a needed sub-skill file is
   missing from the folder, say so plainly instead of improvising.
4. Both routes are prompts-only: never add generation commands, API
   calls, or execution steps to a deliverable.
