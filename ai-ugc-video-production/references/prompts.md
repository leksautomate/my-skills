# AI UGC Video Production — Prompts Only

Source: agent-media-skill (https://github.com/yuvalsuede/agent-media-skill)

IMPORTANT: The original skill contains NO internal/hidden AI generation prompts.
The word "prompt" appears in it only once — as the description of the
`-g, --generate-script <prompt>` option. The video/image generation prompts
live on agent-media's servers and are not in the repo.

Everything below is ALL the prompt-usable material that was actually in the
skill: the script-generation prompt examples, the script word-count rules,
the script template structures, the acting templates/styles, the subtitle
style descriptions, and every example script — plus ready-to-use prompt
templates built directly from those structures (marked as such).

---

## 1. Script-generation prompt examples (verbatim from the skill)

These are the prompts you feed to script generation (`-g`):

- "A fitness tracker that monitors sleep quality"
- "yoga mat product"

Pattern: just a short product description — the generator writes the script.

## 2. The core script rule (use this in any UGC prompt)

Natural speech is 2.5 words per second. Word count MUST match duration:
- 5s video → 10–12 words
- 10s video → 22–25 words
- 15s video → 33–37 words

Too few words = dead silence / awkward pauses. Too many = rushed, robotic.

For Product Acting and Show-Your-App, the cap is 3 words/second:
- 5s → max 15 words
- 10s → max 30 words
- 15s → max 45 words

Ready-to-use prompt (built from the skill's rules):

> Write a UGC ad script for [PRODUCT]. It is for a [5 / 10 / 15]-second video,
> so write exactly [10–12 / 22–25 / 33–37] words — count them before you
> finish. Sound like a real creator talking to camera, not an ad.
> Structure: [pick a template from section 3]. End with this CTA: "[CTA]".
> Voice tone: [energetic / calm / confident / dramatic].

## 3. Script templates (structures from the skill)

| Template | Structure | Best for |
|---|---|---|
| monologue | Hook → Body → CTA | Direct-to-camera talking |
| testimonial | Problem → Solution → Result → CTA | Customer stories |
| product-review | Intro → Experience → Verdict → CTA | Product reviews |
| problem-solution | Hook → Pain → Solution → CTA | Before/after pain points |
| saas-review | Hook → Walkthrough → Opinion → CTA | SaaS / app reviews |
| before-after | Hook → Before → After → CTA | Transformations |
| listicle | Hook → Tip 1 → Tip 2 → Tip 3 + CTA | Tips and lists |
| product-demo | Intro → Demo → Recap → CTA | Product walkthroughs |

Ready-to-use prompt (built from the structures):

> Write a [TEMPLATE] UGC script for [PRODUCT].
> Follow this exact structure: [STRUCTURE from the table above].
> Mention [PRODUCT] by name 2–3 times. Keep it to [word count for duration].

## 4. SaaS review prompt (rules + example from the skill)

Rules from the skill:
- The product name MUST be in the script, and mentioned 2–3 times
- Script word count must match duration (2.5 words/sec)
- The review needs 1–3 product screenshots, named descriptively
  (e.g. `postiz-dashboard.png`, `postiz-calendar.png` — never
  `screenshot1.png`), because images are matched to scenes by filename

Example script (verbatim, 10s, for Postiz):

> "Postiz is the best social media tool I've used. Postiz schedules across
> twenty-five platforms with AI. Try Postiz today."

Ready-to-use prompt (built from the skill's flow):

> Write a 10-second SaaS review script (22–25 words) for [PRODUCT NAME].
> Structure: Hook → Walkthrough → Opinion → CTA.
> Mention [PRODUCT NAME] 2–3 times. Sound like a genuine user, angle:
> [enthusiastic / honest / skeptical-turned-convinced].

## 5. Example UGC scripts (verbatim from the skill)

Basic UGC:
- "Ever wonder why some videos go viral? Here's the secret..."
- "Ever wonder why some videos go viral?"

PIP (picture-in-picture) mode:
- "Stop scrolling. If you struggle to grow on social media, consistency
  beats perfection every time."
- "Three things I wish I knew before starting my business..."

Show Your App:
- "You really need to try this app — it generates UGC videos in seconds."
- "Try this app, it changed everything for me."

Product Acting:
- "I did not expect this perfume to smell this expensive."
- Product description used to generate a script (`--about`):
  "A premium perfume with a warm vanilla dry-down"

## 6. Product Acting prompts (templates & styles from the skill)

Scenario templates (`--template`):
- product-in-hand (default) — actor holds/presents the product
- mirror-selfie
- bathroom-reaction
- kitchen-counter
- car-selfie
- couch-review
- expert-interview
- product-closeup

Acting styles (`--acting-style`):
- raw-selfie (default)
- shocked
- angry
- excited
- dramatic
- weird-hook
- casual-demo
- honest-review

Ready-to-use prompt (built from the skill's fields):

> Create a product-acting UGC prompt: a creator in a [TEMPLATE scenario]
> holding [PRODUCT NAME] — [PRODUCT DESCRIPTION].
> Delivery: [ACTING STYLE]. Extra direction: [visual style — pose, camera,
> environment]. Script (max 3 words/sec × duration): "[SCRIPT]"
> — or generate the script from the product description.

## 7. Subtitle styles (the 17 style prompts/descriptions in the skill)

Popular:
- hormozi — Bold white, yellow karaoke highlight — business/marketing
- tiktok — Bold white, orange-red karaoke — TikTok-style UGC
- minimal — Light, fade in/out — professional, subtle
- clean — White text on dark box — clean readability

Bold & energetic:
- bold — Cyan neon outline, karaoke — high energy
- impact — Huge text, 2 words at a time — short punchy clips
- fire — Red-orange karaoke, dark red outline — hype/excitement
- pop — Yellow text, 2 words at a time — attention-grabbing
- spotlight — Gold highlight, deep shadow — premium/luxury

Aesthetic & soft:
- aesthetic — Subtle, lowercase, airy — lifestyle/beauty
- pastel — Soft pink tones — feminine/soft content
- glow — Purple-pink glow outline — night/party vibes

Colorful:
- neon — Green neon text — tech/gaming
- electric — Cyan text + magenta highlight — bold creative
- gradient — Blue-to-coral karaoke — modern/trendy
- karaoke — Green word-by-word — karaoke-style
- boxed — White bold on solid black box — maximum contrast

## 8. Other prompt inputs the skill uses

- Voice tones: energetic, calm, confident, dramatic
- Background music genres: chill, energetic, corporate, dramatic, upbeat
- Aspect ratios: 9:16, 16:9, 1:1
- PIP overlay options: position bottom-center / bottom-left / bottom-right;
  size small (40%) / medium (55%) / large (70%); animation slide-up /
  slide-left / slide-right / fade / scale; frame none / rounded / shadow
- CTA: a short end-screen line, e.g. "Follow for more", "Try it free"
- Persona: a saved voice sample + face photo combo, reused by name
