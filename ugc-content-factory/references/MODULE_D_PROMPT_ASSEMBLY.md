# Module D (Prompts Only) — Prompt Assembly

Extracted from MODULE_D_ENGINEER.md in
https://github.com/TheMattBerman/ugc-factory-skill

PROMPTS ONLY: all fal.ai execution has been removed from this version — no
endpoints, no queue submission, no API key, no generation. What remains is
only the part that builds the actual video prompt text, so the finished
prompts can be pasted into any video generator (Kling or otherwise).

---

## Prompt formula

```
[Camera] + [Subject doing action] + [Environment] + [Lighting/Texture] + says '[dialogue from Module C]'
```

Merge the Visual Beat Sheet (camera/action, Module B) with the
Synchronized Script (dialogue, Module C) into one prompt per shot.

## Multi-shot prompt assembly (multi_prompt)

```json
{
  "duration": "[total seconds from beat sheet]",
  "aspect_ratio": "9:16",
  "generate_audio": true,
  "shot_type": "customize",
  "multi_prompt": [
    {
      "prompt": "[Camera from Beat Sheet], [Subject action from Beat Sheet], [Environment from Beat Sheet], [Lighting], [Texture], says '[Script from Module C]'",
      "duration": "[shot duration from Beat Sheet]"
    }
  ],
  "elements": [
    {
      "frontal_image_url": "[character reference URL]",
      "reference_image_urls": ["[additional angles if available]"]
    }
  ],
  "negative_prompt": "blur, distort, low quality, studio lighting, professional audio",
  "cfg_scale": 0.5
}
```

### Assembly rules

1. Each `multi_prompt` entry = one shot from the Visual Beat Sheet
2. Prompt formula: `[Camera] + [Subject doing action] + [Environment] + [Lighting/Texture] + says '[dialogue]'`
3. Duration comes from the Beat Sheet (3s, 4s, or 5s per shot)
4. Total duration must equal the sum of all shot durations
5. Never include both `prompt` and `multi_prompt` — use one or the other
6. Minimum shot duration is 3 seconds

## Single-prompt (image-to-video) variant

```json
{
  "prompt": "[Full scene description with dialogue]",
  "start_image_url": "[seed image URL]",
  "duration": "[total seconds]",
  "aspect_ratio": "9:16",
  "generate_audio": true,
  "elements": [
    {
      "frontal_image_url": "[character reference URL]",
      "reference_image_urls": ["[additional angles]"]
    }
  ],
  "negative_prompt": "blur, distort, low quality, professional lighting"
}
```

## Referencing characters/products in prompts

Reference saved characters/products in prompt text as `@Element1`,
`@Element2`, etc. — and always anchor them physically in the scene
(see Module B, Element2 Placement):
- Good: "laptop screen showing @Element2 dashboard"
- Bad: "@Element2 dashboard visible"

## Negative prompts (verbatim from the source)

- Multi-shot / text-to-video: "blur, distort, low quality, studio lighting, professional audio"
- Image-to-video: "blur, distort, low quality, professional lighting"
- Test example: "blur, distort, low quality, studio lighting, professional audio, perfect skin"

## Worked example prompt (verbatim, from the source's test script)

```
Woman in her 30s sitting in bright kitchen, talking to camera with warm
genuine smile, natural window light, casual sweater, authentic UGC selfie
style, slight room reverb in audio
```

## Prompt parameters worth stating with a prompt

| Parameter | Values / default |
|---|---|
| duration | "3"–"15" per generation/chunk; shots are 3s, 4s, or 5s |
| aspect_ratio | "16:9", "9:16", "1:1" (9:16 for UGC) |
| generate_audio | true |
| cfg_scale | 0.5 (prompt adherence 0–1) |
| shot_type | "customize" when using multi_prompt |

## Chunking prompts for videos over 15 seconds (structure only)

Chunk around story beats, not mechanical 15s intervals. The product chunk
(where @Element2 appears) is the anchor point.

Example — 25s video, product appears at ~20s:
- Chunk 1 (0–15s): story setup, no product — character only
- Chunk 2 (15–22s): product reveal — character + product
- Chunk 3 (22–25s): closing/CTA — character, seed frame from prior chunk

Note from source: custom voice IDs and Elements cannot be combined in one
generation, which is why long videos alternate chunk types. For prompt
writing, this just means: keep the product in its own chunk.

## Compilation checklist (prompt content only)

- [ ] multi_prompt array has the correct number of shots
- [ ] Each shot has both `prompt` and `duration`
- [ ] No top-level `prompt` field when using multi_prompt
- [ ] All durations are strings ("3", "4", "5"); sum equals total duration
- [ ] Visual descriptions match the approved Beat Sheet
- [ ] Dialogue matches the approved Script
- [ ] Negative prompt includes anti-studio terms
- [ ] Aspect ratio is 9:16, generate_audio is true, cfg_scale is 0.5
