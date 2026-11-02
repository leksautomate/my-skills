<inputs>
Ask me which animal I want, or pitch 3 animals that each have one insane true fact. Ask which image model I have (any model that takes a reference image works) and whether I want a paid voice (ElevenLabs) or a free one (Kokoro). Then write a 30-35 s script and a shot plan, and show me both before you generate or spend anything.
</inputs>

<direction>
A 1080x1920 cartoon animal-facts short. The art is flat 2D cartoon: thick dark brown outlines, flat colours with simple cel shading, big expressive eyes, vector look. Characters are cutouts that move over illustrated backgrounds, and the place changes every 2-3 s.
Captions are a white pill centred at y 1470: Luckiest Guy 66px, ink text #1f1418, pill height 1.55x the font size, a 7px ink outline, 2-3 words per chunk. One key word per chunk is yellow #ffd21f with an ink stroke 0.14x the font size. Each chunk pops in from 0.82 scale in 0.13 s with a back ease.
Big title words sit at y 430 in Luckiest Guy 104-170px. The ink stroke is 0.22x the size, with a darker copy 0.09x the size underneath. Pairs: yellow #ffd21f/#c27a10, red #ff4a3d/#8e1a14, pink #ff7ab8/#a8336d, white #ffffff/#9aa6b4. They spring in, scale 1 - 0.6·e^(-9t)·cos(20t), then wobble ±1.4°.
Annotations are a red marker ring (20px ink + 11px #ff3b30, tilted -7°) and a curved red arrow (26px ink + 13px red). Hits are a yellow and white starburst with white speed lines. Every water or air scene has drifting specks, and every scene has a soft vignette.
Banned: any frame where nothing moves for 1 s, slow push-ins on a still, characters baked into backgrounds, realistic rendering, gradients on text, emoji, full stops in titles.
</direction>

<structure>
Length: the voice decides, 30-35 s at about 3.5 words per second, one fact per sentence, with a joke metaphor for each fact.
0 s the hook asks "why does this animal do [weirdest fact]?" while the character does it on screen. The red ring draws around the subject on the word that names it, and the hit lands on the verb with a starburst, a title word and a shake → the name card: the animal enters with speed lines and its name slams in as a title → a contrast beat (monster, giant, deadly) on a new background, with a 1.1 zoom punch and a shake on the key word → a real-world size comparison (a fingertip, a phone, a bus) with a curved red arrow and the measured number → each next fact gets its own metaphor scene (an empty nightclub for "rare", a wedding for "many partners", a bouncer for "defences", a checklist card for "what it loses", a counter popping 1 to N for numbers). Every fact gets a new background or framing, a pose swap on its key word, one title word and one sound → the grossest or most shocking fact gets the biggest title and a sad trombone → the last line flips the hook into a punchline, with one big final move (a giant heart, an explosion) and the title held to the end. Cut every 1.5-3 s; inside a shot, something new happens every 0.5-1 s.
</structure>

<build>
1. Tools: Python, Playwright with Chromium, FFmpeg, faster-whisper, OpenCV, Pillow. Install what's missing and tell me what you installed.
2. Art, only 2 images:
   - Pose sheet: one 1:1 image at 2K, "a 3 by 3 pose sheet, 9 separate poses on plain pure white, plenty of white space, nothing touching, no grid lines, no text, no ground shadows".
     - The 9 poses: neutral, yelling with the mouth open, shocked, embarrassed with a blush, in love with heart eyes, worried with a sweat drop, attacking, a ruined or shrivelled version for the payoff, and one side character. All face the same way; flip them in code.
     - Image models often draw one character in every cell. If that happens, make the second character in code: recolour it in Lab space and cut or add features.
   - Background grid: one 9:16 image at 4K, with the pose sheet as the style reference, "a 3 by 3 grid of 9 equal tall panels separated by thin white gutters, each an EMPTY scene, no characters, no text, keep the lower middle open".
     - Split it on the white gutters (rows and columns whose min-channel mean is over 232), crop 4px in, Lanczos to 1080x1920, then unsharp at radius 2, 60%.
3. Cutouts:
   - Flood the white from the border with a floating range of 7 per channel; this also removes soft glows. Add manual seeds for white pockets enclosed by fins or limbs.
   - Make a 3px soft alpha band outside each shape at (250 - min channel) / 150, then un-mix the white from the edge pixels.
   - Group connected components by grid cell, crop and save PNGs.
   - If a pose touches the sheet edge, graft the missing part from another pose with a template match.
4. Voice: ElevenLabs eleven_v4 (one take) or Kokoro.
   - Cut every pause over 0.2 s down to 0.13 s, only where loudness is under -40 dB in 10 ms windows.
   - Speed it up with ffmpeg atempo (about 1.14) until it lands at 30-33 s.
   - Run faster-whisper small.en with word timestamps on the FINAL file and write words.js. Every cut, pose swap, title and sound starts on a real word's start time.
5. Film: one HTML canvas where every frame is a pure function of time. Expose window .seek(t), window.READY once fonts and images have loaded, window.END, and window.EV with the event times for every sound.
   - Characters: draw each cutout with position, scale, rotation and flip.
     - Swim or walk by drawing it in 28 vertical slices, each offset by sin(8t - 4.5u) times 10px (14px while darting), weighted ((u - 0.3) / 0.7)^1.5 toward the tail.
     - Idle bob is 10px at 2.7 rad/s plus a ±0.035 rad tilt.
     - A pose swap is an instant image swap with a squash of 1 + 0.18·e^(-10t)·cos(22t).
     - Entrances ease out (cubic) over 0.3-0.5 s, with 5 white speed lines, 9px wide, 34px apart.
     - A hit is a 24-point yellow and white starburst (radius 105px or less, never over a face), 10 flying lines over 0.45 s, and a camera shake of 22-34px decaying at e^(-7t).
     - Anything attached to a character is placed in that character's local space, so it moves with it. Draw order decides behind and inside.
   - Camera: setTransform with a zoom and a focus point. Use 1.1 zoom punches on key words and 1 to 1.4 push-ins over 2 s. When the camera zooms onto a background feature, draw that background in world space so it doesn't slide.
   - Backgrounds: cover-fit, drifting 1-2% zoom per second. Add 40 specks (2-6.5px, alpha 0.45, rising 14-50px/s) and a 0.35-0.55 vignette.
   - Props in code: the red ring (draws on in 0.28 s), the curved arrow, a checklist card with red X stamps, counters popping 1 to N, rising hearts, a puff cloud for transformations, and simple shapes like DNA, a tumbleweed, or a vessel with flowing cells.
6. Render:
   - Playwright Chromium with --allow-file-access-from-files calls seek for every frame at 60 fps, with 6 motion-blur subframes over half a frame, blended at globalAlpha 1/(i+1).
   - Pipe JPEG frames into ffmpeg libx264 at CRF 16.
   - Before the full render, show me a contact sheet of 12-15 frames and fix anything covered, off-frame or not moving.
7. Sound:
   - Music: one bouncy cartoon track (free on Pixabay), sitting 7-10 dB under the voice in every phrase.
   - SFX: one downloaded Mixkit sound per event. Whoosh on entrances, chomp or impact on hits, pop on titles, boing on landings, kiss on hearts, sad trombone on the gross fact, fail buzzer on rejections, poof on transformations, bubbles in water scenes.
   - Mix to about -14 LUFS, then re-encode at CRF 21 for upload.
</build>

<gotchas>
Image models ignore "two different characters" more often than not, so plan the recolour from the start. Don't name your draw function frame, because the renderer's capture hook may use window.frame. Whisper splits compound names ("angler fish"); merge them before you match captions, and check that the caption word count equals the transcript's. A still pose for over 1 s reads as AI slop, so everything on screen bobs, wiggles or reacts every frame.
</gotchas>

<start>
Ask me for the animal, or pitch 3, then show me the script and the shot plan.
</start>
