# Animify: An Audio-Reactive 3D Music Player

Animify is a web-player featuring true audio reactive multi-mood visualizers via Web Audio API in local mode. Users can also connect Spotify (requires premium), to playback music while retaining all the visualizers and moods backed by a fake synthesizer. It also features a dynamic contrast changing UI and accessibility settings.  

[Live Demo]
[LinkedIn Post]

## Features
1. **Moods:** Features 4 different moods to choose from - **Chill, Energy, Focus, Neutral.** All containing different visualizers and frequency settings. 
2. **Dynamic Backgrounds:** Using in-built Spotify call tools or downloading album arts for local mode, the web-player constantly changes the background to the album art of the song currently playing. Ensuring the visualizers are always fresh and don't get boring.
3. **Local Mode:** This mode works when Spotify is not connected and has true-audio reactive visualizers. Users can also add their own files (instructions provided in the Local Setup section). This is achieved via `Web Audio API` and `AnalyzerNode`. 
4. **Spotify SDK Integration:** Users can connect their Spotify for playback inside the web-player using secure `oAuth 2.0` login. (This feature requires Spotify subscription.)
5. **Fake Synthesizer:** Spotify deprecated the `Audio Wave Analysis API` in late 2024, due to misuse by genAI. So I came up with the idea of a fake synthesizer, which always runs on a base 120bpm, and gives fake wave signal, to create an illusion of audio reactivity when Spotify playback is active. 
6. **Dynamic Contrast Changing UI:** Based on the background, the UI changes the colour in real time, so every button is visible at all times, no matter how dark or bright the background gets. 
7.  **Volume Matching And Visual Boost:** The visualizer strength is directly connected to the volume and values set by the user under the "Audio" and "Boost" section in the webpage respectively.
8. **Accessibility Settings:** Includes extensive accessibility settings, to ensure a compatible experience for every user. 



## How it works
### Web Audio API & Frequency Extraction:
- Before sending data to react libraries containing the shaders and visualizers, the wave data needs to be precisely seperated and cleaned. For this purpose `Web Audio API` and the node it provides, `AnalyserNode` was used.
- `Web Audio API` creates an `AudioContext` file for each song, within which `AnalyzerNode` is used to extract frequency and wave data from the raw data provided by `SourceNode` using **Fast Fourier Transfer Analysis**, seperating each frequency into sub-frrquency set- `subbass`, `bass`,`mid`,`high`, and `impact`.
- After each frequency is sorted into each category, each frequemcy is then further grouped into `FFT size` or commonly known as **bins** of 20hz. It is on these bins where comparisions are made and passed onto react shaders.
- The code calls for `getByteFrequencyData()` and `getByteTimeDomainData()`, where `getByteFrequencyData()` represents raw frequencies and `getByteTimeDomainData()` represents transient density, or volume spikes in simple words. The code runs an `ANDgate` logic multiple times per-second to check whether there was a change in frequency bins and their volume spike. If change is detected above 5% threshold, the values change to 1, signaling the shader to react to the audio


### Mood Scenes & Visualizers:
1. **Chill:**
      - [Explain the layered planes (Deep, Warm, Light), liquid Simplex noise displacement, mouse-reactive parallax, `<Sparkles>`, `<Float>`, and the warm amber color grading...]
2. **Energy:**
      - [Explain the RGB channel splitting (Red, Green, Blue on separate planes), kinetic mouse-driven offsets, `<MeshDistortMaterial>` blob, and post-processing (Bloom, ChromaticAberration, Glitch)...]
3. **Focus:**
      - [Explain the clean single-plane design, gentle desaturation, vignette, and the intentionally minimal/static aesthetic...]
4. **Neutral:**
      - [Explain the raw static background with zero shaders/animations, pure album art display...]

### The Fake Synthesizer:
- **The Problem:** [Explain that Spotify deprecated the `Audio Wave Analysis API` in late 2024, and CORS/DRM blocks `AnalyzerNode` on cross-origin streams...]
- **The Solution:** [Explain how `useChillSynthesizer.ts` uses deterministic math — layered sine waves, Perlin noise, and `currentTime` — to generate simulated bass, mid, high, and impact values that mimic the real frequency bands explained above...]

### Custom GLSL Shaders:
- [Explain vertex and fragment shaders, `coverUv` aspect-ratio math, Simplex noise displacement, desaturation, and vignette — all written by hand, no third-party shader files...]

### Texture Lifecycle & Memory Management:
- [Explain how `useTrackTextures.ts` loads images via `THREE.TextureLoader`, uses GSAP to crossfade uniforms, and calls `.dispose()` on old textures to prevent GPU memory leaks...]

### Dynamic Contrast UI:
- [Explain how `useImageBrightness` samples pixel luminance from album art on a hidden `<canvas>` and dynamically switches text/icon colors between black and white...]

### Local Player Engine:
- [Explain how `useLocalPlayer.ts` manages playlist queues, `useRef`-based state for event listeners, and the `useActivePlayer` abstraction layer...]




## Key Commands
| Key / Action | Function |
|---|---|
| `[Key]` | [What it does] |
| `[Key]` | [What it does] |
| `[Key]` | [What it does] |

## Tech Stack
- **Framework and Core:** `Next.js`, `React`, `Node.js`, `TypeScript`, `Vanilla CSS`
- **3D and Graphics:** `Three.js`, `React Three Fiber`, `Drei`, `GLSL`
- **Post-Processing:** `@react-three/postprocessing` (`Bloom`, `ChromaticAberration`, `DepthOfField`, `Glitch`, `Vignette`, `Noise`)
- **Animations:** `GSAP`

## What I learnt and Key Challenges

### Learning:
- [Learning 1]
- [Learning 2]
- [Learning 3]
- [Learning 4]
- [Learning 5]

### Key Challenges I faced:
- **[Challenge 1 Name]:** [Explain the problem and how you solved it...]
- **[Challenge 2 Name]:** [Explain the problem and how you solved it...]
- **[Challenge 3 Name]:** [Explain the problem and how you solved it...]
- **[Challenge 4 Name]:** [Explain the problem and how you solved it...]