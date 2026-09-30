---
name: "almighty-ugc-factory"
description: "Almighty UGC Factory — MASTER UGC skill (PROMPTS ONLY). The single entry point for ALL UGC prompt and script requests. First ASK the user: talking-head script, or multi-shot video with camera direction? Then route to the matching sub-skill: talking-head → ai-ugc-video-production; multi-shot → ugc-content-factory. Trigger on 'UGC', 'Almighty UGC Factory', 'UGC ad', 'UGC video', 'UGC prompt', 'UGC script', 'make a UGC', or any request to create UGC content."
metadata: { "includeInPrompt": true }
---

# Almighty UGC Factory — Master Skill (Prompts Only)

## Purpose
One front door for all UGC work. This master skill contains no prompt
material of its own and does NOT merge the two UGC sub-skills — they stay
separate and unchanged as the source of truth. The master's only job:
ask which style the user wants, then run the matching sub-skill's
workflow exactly as that sub-skill defines it.

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
Skill: `ai-ugc-video-production`
Read `~/workspace/skills/ai-ugc-video-production/SKILL.md` and
`~/workspace/skills/ai-ugc-video-production/references/prompts.md`,
then follow that skill's workflow and output contract:
script templates (monologue, testimonial, product-review,
problem-solution, saas-review, before-after, listicle, product-demo),
2.5 words/sec word-count rule, product-acting scenarios, subtitle styles.
Deliverable: the finished prompt/script text, ready to paste.

### Route B — Multi-shot video with camera direction
Skill: `ugc-content-factory`
Read `~/workspace/skills/ugc-content-factory/SKILL.md` and its
references (Modules A/B/C, Module D prompt assembly, character library,
scene settings), then follow that skill's pipeline:
Creative Brief → Visual Beat Sheet → Synchronized Script → assembled
per-shot video prompts / multi_prompt JSON. Keep its approval gates
unless the user asks for a full one-shot run.

## Operating Rules
1. Never do UGC work "freehand" when a request matches this master —
   always route through one of the two sub-skills.
2. Do not copy sub-skill content into this file; if a sub-skill's
   instructions and this file ever conflict, the sub-skill wins for its
   own route.
3. If the chosen sub-skill is missing, say so plainly instead of
   improvising its workflow.
4. Both routes are prompts-only: never add generation commands, API
   calls, or execution steps to a deliverable.
