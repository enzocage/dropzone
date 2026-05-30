# IO — Dropzone Ultimate Edition

A retro-style side-scrolling rescue game inspired by classic Commodore 64 titles. Pilot your jet across a procedurally-generated wraparound landscape, rescue scientists from the surface, and return them to base — all while fending off waves of hostile aliens.

Zero dependencies. Single HTML file. Runs in any modern browser.

## Features

- **8 enemy types** — Planters, Androids, Nemesites, Spores, Trailers, Blunders, Nmeyes, and Antimatter
- **Procedural world** — wraparound terrain with volcanoes, an ionic lake, and parallax mountain layers
- **4 color palette themes** — Classic C64/Colodore, Cyberpunk Neon, Virtual Boy Red, Matrix Green
- **WebGL CRT post-process** — barrel distortion, scanlines with aperture grille RGB mask, chromatic aberration, vignette
- **Procedural chiptune music** — 3-voice tracker engine (bass, arpeggiator chords, percussion) via Web Audio API
- **15+ sound effects** — entirely synthesized, no external audio files
- **Multi-input support** — keyboard, gamepad, touch/pointer (mobile-friendly with on-screen controls)
- **Persistent settings & high scores** — stored in localStorage
- **Haptic feedback** — for touch devices

## How to Run

Open `dropzone_ultimate_edition.html` directly in any modern browser (Chrome, Firefox, Edge, Safari).

No build step, no dependencies, no server required.

## Controls

| Action | Keyboard | Gamepad | Touch |
|---|---|---|---|
| Move | WASD / Arrow keys | Left analog stick | Left half drag |
| Fire | Space / J / Z | Button 0 | Right bottom tap |
| Shield / Cloak | Shift / C / K | — | Right middle tap |
| Smart Bomb | X / B / L | — | Right top-right tap |
| Pause | Escape / F1 / P | — | — |

## Settings

| Setting | Default | Description |
|---|---|---|
| CRT Filter | On | Retro screen warp and glow |
| Scanlines | On | CRT aperture grille effect |
| Color Palette | Classic | C64, Cyberpunk, Virtual Boy, Matrix |
| Purist Chip | Off | Mutes all music |
| Reduced Motion | Off | Disables particle effects |
| Haptic Vibe | On | Vibration feedback on touch devices |
| Music Volume | 40% | Procedural music level |
| SFX Volume | 65% | Sound effects level |

## Gameplay

**Objective:** Rescue humans scattered across the terrain by picking them up and returning them to the dropzone base.

- Fly low over a human to pick them up, then land at the dropzone to deliver them
- Each rescue awards points, with combo multipliers for successive rescues
- Waves increase in difficulty — every 4th wave is a Trailer Invasion
- Earn an extra life and bomb every 10,000 points
- If all humans die, emergency Antimatter enemies spawn

**Pilot Ratings:**
- Novice → System Cadet → Moon Defender → Omega Star (500,000+)

## Tech Stack

- JavaScript (ES6+) — single HTML file
- HTML5 Canvas 2D for game rendering
- WebGL fragment shader for CRT post-processing
- Web Audio API for procedural audio
- localStorage for persistence
- Gamepad API + Pointer Events for input

## License

© 2024 Dropzone Ultimate Edition. All rights reserved.