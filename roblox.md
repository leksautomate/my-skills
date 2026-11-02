<inputs>
Ask me for: my story in one line ("in this town, [a rule everyone obeys]", plus the real reason the rule exists, which is the twist) and the length (40-50 s). If I have no idea, pitch me 3 rules with their twists and let me pick. Every story is mine, never a copy of an existing video.
</inputs>

<direction>
A 1080x1920 30 fps Short that looks like a Roblox horror story, built entirely in Blender from code with no Roblox assets. The characters are R6 block characters with flat cartoon face decals that you draw. The world is a town at night made of plain parts in saturated flat colours like a screen recording:
- the sky is a gradient from #212B54 at the horizon to #060917 overhead, with tiny stars
- a cold moon (#9EB8FF, strength 0.55)
- grass in two noisy tones (#336B24 to #42802B)
- the road is asphalt #212126 to #2E2E33 with a #FAC726 centre line
- warm practical lights do all the real lighting: streetlamps, lit windows (#FCC773), porch lights and a flashlight
The threat is one thing that is far too tall (about twice the kids' height) and thin, matte black #0D0D0F, with long arms and three long fingers. It has a white glowing face: hollow tilted eyes with no pupils, and a grin far too wide with gaps between the teeth.
Captions show one word at a time in Title Case, in Montserrat ExtraBold at 104px: white, with a 13px black outline and a black shadow 4px right and 7px down at 60% opacity. Key nouns are red #EC1C24. Captions are centred, with their middle at 64% of the screen height.
A deep, firm adult narrator tells it in third person, fast and serious.
Banned: Roblox logos, catalog faces or assets, AI video, motion blur, depth of field, the Filmic or AgX look, full stops in captions, the narrator saying sound words ("clunk", "bang", "creak"), pitching the narrator's voice, glitch, footstep or heartbeat SFX loops, any shot longer than 2.5 s, and any frame where nothing moves.
</direction>

<structure>
Length: 40-50 s at about 210 wpm, about 36 shots, cut every 0.5-2.5 s (median 1.25 s).
0 s the rule in one line over a wide of the town already obeying it → the cost on screen: someone gets caught, vanishes, and only an object is left behind, still moving (a cap rocking on the sidewalk) → an insert of the deadline (a clock ticking over) → everyone obeys: a wide of people running home, then a shutter slams and a door bolts, each in its own close → "But tonight": the hero breaks the rule for someone he loves, he grabs a prop and it clicks on → the chase: the threat closes in toward camera shot by shot, each step lands on its own word, and the hero looks back in a close → he finds them under the last safe thing → "Run!": the music steps up hard on that exact word → the safe place fails (he pounds on the door, nobody answers) → the last safe thing flickers and dies: a riser into one huge boom, then every light, the music and the drone go dead for about 3 s of real silence, with only roofs against the stars → it all comes back with a braam on the same wide as the opening, but wrong (every door open, every house empty, a chair still rocking) → the twist line, the real reason for the rule, over a close two-shot → the hero turns slowly to his own door, which creaks open onto black → the tall thing bends down out of it, then a shot from its height looking down onto two terrified faces → it says one short line, its head snaps sideways on the last word, a trailer hit lands with a sting on top, and the last shot holds 1.5 s.
</structure>

<build>
1. Tools. Everything is free and local except the voice. Install what's missing and tell me what you installed:
   - Blender 4.2 or newer as the portable zip, run headless with `blender -b --factory-startup --python build .py -- MODE OUT`
   - Python with numpy and Pillow
   - FFmpeg
   - faster-whisper with large-v3-turbo, int8 on the CPU
   - an ElevenLabs API key (ask me for it, and never print it)
   - the Montserrat font
   - free sounds from Pixabay or Mixkit:
     - one tense horror music bed with a hard step-up somewhere in it, and a low horror drone
     - big hits: a deep impact, 2 sub drops, 2 cinematic booms, a horror riser, a braam, a horror door creak, a trailer hit and a horror sting
     - quiet foley: a shutter slam, a door slam and door knocks
2. Voice:
   - Write about 22 short lines per 45 s and show me the script before you record. The narrator never says a sound word; the SFX carry every sound.
   - Ask before spending credits. Make one ElevenLabs take with eleven_multilingual_v2 and the premade voice "Adam" (Dominant, Firm), all lines in one request so the read flows.
   - Pauses:
     - Cut only in real silence: below -44 dB for at least 0.06 s. Keep 35 ms of audio either side of every cut.
     - Between lines: 0.06 s plus 0.08-0.30 s (the longest goes right before the twist).
     - Inside a line: 0.11 s.
     - After the blackout word: 0.95 s.
   - Speed it up 1.15-1.25x with atempo only, so the read lands at about 36 s. Never change the narrator's pitch or formants.
   - The monster's line: split it off and pitch it 5 semitones down. Slow it to 0.92x, add a short room echo (55 and 110 ms), apply a lowpass at 6.5 kHz, and put it 0.22 s after the narration.
3. Timing:
   - Run faster-whisper with word timestamps on the final voice file and match it to the script with difflib.
   - Key every cut, light death, pose snap and SFX to a word index, never to a fixed second.
   - Cuts land 0.04 s before their word. A light dies 0.06 s after its word, flickering for 0.12 s first (two sines at 61 and 37 rad/s, lit while their sum is above -0.25).
4. Characters and world, built from boxes:
   - Kids:
     - Body pivot at height 2. Torso 2x1x2.
     - Arms: 1x1x2, from shoulder pivots at x ±1.5.
     - Legs: 1x1x1.62, plus 1.02x1.04x0.38 shoes, from hip pivots at x ±0.5.
     - Head: a cylinder of radius 0.62 and height 1.22 with a 0.22 bevel.
     - The younger sibling is the same rig at 0.8 scale.
     - Faces: draw them in Pillow at 1024x578 with flat black strokes, keeping the features in the middle 45%, and map them onto the front 130° of the head. At least: smile, stern, angry, scared, panic, shock and determined.
   - The monster:
     - Legs: 0.62 thick and 4.4 tall.
     - Chest: 1.6x0.7x3.4.
     - Head: radius 0.86 and 1.8 tall.
     - Arms: 5.8 long, with three 1.1 fingers on each hand.
     - Its face decal is white and emissive, so it glows in the dark.
   - Streetlamps:
     - 13.2 tall, 30 apart.
     - Each is a warm #FFBD6B spot light of 4200 W in a 118° cone, with a bulb of emission 9 that swaps to a dead grey bulb.
     - The last light is one globe: a 9000 W point light with emission 14.
   - Other lights:
     - Porch lights: 650 W.
     - The flashlight: a 1400 W spot in a 34° cone, plus a beam cone at 6% alpha.
   - The blackout:
     - Every lamp, window, porch light and the flashlight goes off.
     - The sky drops to 12% and the moon to 0.04.
5. Animation: one key per frame at 30 fps with constant interpolation, on every light and material too, so everything snaps like Roblox.
   - Poses hold, then snap with a back ease (overshoot 2.2) over 0.12-0.16 s. Swap the face on the same frame.
   - Run: 2.5 Hz, legs ±52°, arms ±58°, a 9° lean. The flashlight arm is held out at -52°.
   - Empty shots still move:
     - Swings drift at 0.33-0.42 Hz, ±7-16°.
     - The rocking chair rocks at 0.75 Hz, ±9°.
     - The clock's second hand ticks.
   - The monster bends 72° at the hip over its shot. On the last word its head snaps 24° sideways with a back ease in 0.14 s.
6. Shots:
   - Use a vertical sensor fit, so fov is vertical: 32-44° for closes, 46-56° for mediums, 58-70° for wides.
   - The camera is mostly locked, with smoothstep push-ins and one slow slide along the empty houses.
   - Render Eevee at 32 samples with shadows and ray tracing on, using the Standard view transform at exposure 0.
   - Before the full render, look at a 50% still at 12 samples from the middle of every shot.
   - The threat shots must read on a phone: the light dying behind the hero, the dark moving toward camera.
7. Edit and sound:
   - Captions: each word appears 0.03 s before it's spoken and stays until the next. Hold the last word 0.25 s, and strip punctuation.
   - Levels:
     - Voice: the speech median at -15 dB.
     - Music bed: -21 dB RMS, ducking 4 dB under every word (fast attack, about 0.25 s release). Start it so its step-up lands on "Run!".
     - Drone: -34 dB under the bed.
   - The bed and drone cut dead on the blackout word. The bed comes back quiet with the lights, then fades out 0.5 s before the monster speaks.
   - SFX: only about 1 big hit every 7-10 s, each one downloaded and trimmed so its peak lands on its word:
     - the first vanishing: deep impact at -15
     - each step of the chase: sub drops at -14 and -17
     - foley: -18 to -21
     - the last light: riser at -21 into a boom at -15, then the big boom at -11
     - the lights coming back: braam at -15
     - the door: creak at -18
     - straight after the monster's last word: trailer hit at -11 plus a sting at -19
   - Mix to -13 LUFS, then apply a tanh soft clip at 0.75 so it lands at -14 after AAC. Encode H.264 (slow preset, CRF 17, maxrate 6M, yuv420p) with AAC at 256k.
</build>

<gotchas>
Convert every colour from sRGB to linear before it goes into Blender, or everything renders washed-out grey-blue. Give Blender an absolute output path. Lights fade between keys unless every key, including light energy and material emission, is set to constant. In Blender 4.4 and newer, actions keep their fcurves inside layers, strips and channelbags, so `action.fcurves` is gone. Whisper swallows pauses into the next word, so find silences in the audio itself and give each word gap the longest silence near it. A full render takes about 2 s a frame at 1080x1920, so do the stills pass first, and re-render only the frame ranges that changed.
</gotchas>

<start>
Ask me for my story first (or pitch me 3), then show me the script before you spend any voice credits.
</start>
