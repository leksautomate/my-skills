---
name: "ugc-content-factory"
description: "UGC Content Factory — PROMPTS ONLY. Director-first UGC prompt writing using the modules from TheMattBerman/ugc-factory-skill: Creative Director brief, Cinematographer visual beat sheet with Kling video prompts, Screenwriter dialogue synced to shots, character library, scene settings, and multi-shot prompt assembly. No video/image generation, no fal.ai, no API key. Trigger on 'ugc factory', 'ugc content factory', 'Kling prompt', 'UGC video prompt', 'testimonial video prompt', or 'director-first UGC'."
metadata: { "includeInPrompt": true, "source": "https://github.com/TheMattBerman/ugc-factory-skill" }
---

# UGC Content Factory — Prompts Only

## Purpose
Write complete UGC video prompts — creative brief, visual beat sheet,
per-shot video prompts, synced dialogue, and assembled multi-shot prompt
JSON — using the director-first method from the source skill.
This installed version is PROMPTS ONLY: it does NOT generate videos or
images, does NOT call fal.ai, and needs no `FAL_KEY` or credits. Where a
reference file mentions generating images, uploading to fal.ai, or locking
Elements, treat that step as "write the prompt for it" and stop there.

Source: https://github.com/TheMattBerman/ugc-factory-skill
(upstream name: ugc-content-factory, by Matthew Berman)

## Pipeline (prompt writing, with approval gates)

```
MODULE A: Creative Director  → Creative Brief       → GATE 1
MODULE B: Cinematographer    → Visual Beat Sheet    → GATE 2
MODULE C: Screenwriter       → Synchronized Script  → GATE 3
MODULE D: Prompt Assembly    → multi_prompt prompts → Output (text/JSON only)
```

Do not skip gates unless the user asks for a full one-shot run.

## Modules

1. **Module A — Creative Director** (`references/MODULE_A_CREATIVE_DIRECTOR.md`,
   plus `references/CHARACTER_LIBRARY.md` and `references/SCENE_SETTINGS.md`):
   pick ONE format (Testimonial, Unboxing, Problem/Solution, Comparison,
   Demo), ONE hook angle (Gatekeep, Skeptic, Fail, Visual Shock), character
   archetype + setting. All 4 stealth checks must pass: Camouflage, Vibe,
   Integration, Imperfection.
2. **Module B — Cinematographer** (`references/MODULE_B_CINEMATOGRAPHER.md`):
   visuals BEFORE script. Shot-by-shot beat sheet, shots of 3s/4s/5s, the
   6 prompt elements (Camera, Subject, Environment, Lighting, Texture,
   Emotion), the 4 Kling prompting rules, and the Photorealistic
   Pre-Prompt + Nano Banana image prompt structure for character/seed
   images (write the image prompts; do not generate the images).
3. **Module C — Screenwriter** (`references/MODULE_C_SCREENWRITER.md`):
   the beat sheet is locked — write dialogue to fit it. ~2.5 words/sec
   (3s = 7–8 words, 4s = 9–10, 5s = 12–13), authentic cadence with filler
   words, no ad-speak, product name once, maybe twice.
4. **Module D — Prompt Assembly** (`references/MODULE_D_PROMPT_ASSEMBLY.md`):
   merge beat sheet + script using the prompt formula
   `[Camera] + [Subject action] + [Environment] + [Lighting/Texture] + says '[dialogue]'`
   into per-shot prompts / a `multi_prompt` JSON, with the negative prompt
   "blur, distort, low quality, studio lighting, professional audio".
   Deliver the prompts as text/JSON — never submit them anywhere.

## Output Contract
- Gate outputs in the source formats (Creative Brief, Visual Beat Sheet,
  Synchronized Script), then the final assembled video prompts.
- Every per-shot video prompt: 1–3 sentences, leads with camera movement,
  names real light sources, includes texture, describes temporal flow.
- No generation, API calls, or execution steps in the deliverable.
