---
name: "ai-ugc-video-production"
description: "AI UGC video production — PROMPTS ONLY. Write UGC ad prompts and scripts (script templates, word counts, product-acting scenarios, subtitle styles) using the material extracted from the agent-media skill. No video/image generation, no CLI, no login, no credits. Trigger on 'AI UGC', 'UGC prompt', 'UGC script', 'SaaS review script prompt', 'product acting prompt', or 'show your app script'."
metadata: { "includeInPrompt": true, "source": "https://github.com/yuvalsuede/agent-media-skill" }
---

# AI UGC video production — Prompts Only

## Purpose
Produce prompts and scripts for UGC-style videos only. This skill does NOT
generate videos or images, does NOT use the `agent-media` CLI, and needs no
login or credits. The original agent-media skill contained no hidden/internal
generation prompts — its generation prompts are server-side. All prompt-usable
material from it is extracted in `references/prompts.md`.

## Workflow
1. Read `references/prompts.md` for the templates, rules, styles, and examples.
2. Pick a script template (monologue, testimonial, product-review,
   problem-solution, saas-review, before-after, listicle, product-demo) and
   follow its structure.
3. Match word count to duration exactly: 2.5 words/sec for UGC scripts
   (5s = 10–12 words, 10s = 22–25, 15s = 33–37); max 3 words/sec for
   Product Acting / Show-Your-App scripts. Count the words before delivering.
4. For SaaS reviews: product name in the script, mentioned 2–3 times.
5. Deliver the prompt/script text only — no generation commands.

## Output Contract
- The finished prompt(s) and/or script(s), ready to paste into any generator.
- State the template, duration, and word count used when it matters.
- No CLI commands, API calls, pricing, or generation steps.
