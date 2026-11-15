# Retro Sisters

A complete, original 2D retro jump'n'run game in the style of classic C64 platformers — built as a **multi-agent AI experiment** coordinated by Hermes.

100 % original: custom procedural pixel art, custom level maps, custom SID-style music.
**No** Giana Sisters or other copyrighted material, sprites or level maps.

## Run it (Zorin / any Linux)

Open `index.html` directly in your browser:

    firefox ~/projects/retro-sisters/index.html

or via a local-only preview server (nothing publicly reachable):

    python3 -m http.server 8000 --directory ~/projects/retro-sisters

No build step, no external libraries, no network access needed.

## Controls

| Action | Keys |
|---|---|
| Run | A/D or ←/→ |
| Jump | Space, W, ↑ (coyote time + jump buffering) |
| Start | Enter/Space or Start button |
| Pause | P or Esc / Pause button |
| Music/SFX toggle | Buttons under the canvas |

## Multi-agent experiment

This project documents a coordinated multi-agent workflow:

- **Hermes** — project lead and coordination (scope enforcement, backups, verification)
- **Qwen** — composed the SID-style music track *"Chrome Circuit"* (32 bars, 150 bpm, 3 voices, 51.2 s seamless loop)
- **Codex** — implementation of the composition into the SID engine and technical code review
- **Claude Code** — independent reviews of game logic, music and code
- **Claude Fable 5.2** — the graphical overhaul (pixel art, animations, parallax backgrounds, C64 palette)

The final version was **successfully tested in the browser on Zorin OS** by the user.

## Features

- Tile-based world, 16 px logical tiles, 60 fps fixed-timestep physics, AABB collisions
- 3 themed levels (Sunlit Orchard / Moonlit Rooftops / Crystal Cave) with multi-layer parallax backgrounds
- Player with 8-frame run cycle, blinking idle, jump poses, star-power variants
- Enemies (per-world recolored beetles, stompable), spinning gems, pulsing power star, waving flag
- Custom 5×7 pixel font, C64-family 16-color palette, C64-style overlay windows
- Authentic C64 SID emulation in `audio.js` (3 voices + bass noise, pulse/sweep/triangle/LFSR-noise,
  ADSR, filter table, controllable vibrato, 3-note arpeggios, *"Chrome Circuit"* loop + 7 SFX)
- Game runs fully silent and playable if audio is unavailable (`window.__SID` guarded)

## Files

- `index.html` — the entire game (inline JS, loads `audio.js` first)
- `audio.js` — self-contained SID chiptune engine (`window.__SID` API)
- `composition.json` — Qwen's *"Chrome Circuit"* note notation (source data for the music)
- `CHANGELOG.md` — full development history (v1.0 → v1.6)

## Deutsch

Ein komplette, originalen 2D Retro Jump'n'Run in klassische C64-Plattformjumper-Style — as a **multi-agent KI experiment** coordinated by Hermes.

100 % Original: Procedural Pixel Art (own), own Level Maps, own SID-Style Music.
**No** Giana Sisters or other copyrighted material, sprites or level maps.

## Run it (Zorin / any Linux)

Open `index.html` directly in your browser:

    firefox ~/projects/retro-sisters/index.html

or via a local-only preview server (nothing publicly reachable):

    python3 -m http.server 8000 --directory ~/projects/retro-sisters

No build step, no external libraries, no network access needed.

## Controls

| Action | Keys |
|---|---|
| Run | A/D or ←/→ |
| Jump | Space, W, ↑ (with coyote time + jump buffering) |
| Start | Enter/Space or Start button |
| Pause | P or Esc / Pause button |
| Music/SFX toggle | Buttons under the canvas |

## Multi-Agent-Experiment

This project documents a coordinated multi-agent workflow:

- **Hermes** — project lead and coordination (scope enforcement, backups, verification)
- **Qwen** — composed the SID-style music track *"Chrome Circuit"* (32 bars, 150 bpm, 3 voices, 51.2 s seamless loop)
- **Codex** — implementation of the composition into the SID engine and technical code review
- **Claude Code** — independent reviews of game logic, music and code
- **Claude Fable 5.2** — the graphical overhaul (pixel art, animations, parallax backgrounds, C64 palette)

The final version was **successfully tested in the browser on Zorin OS** by the user.

## Features

- Tile-based world, 16 px logical tiles, 60 fps fixed-timestep physics, AABB collisions
- 3 themed levels (Sunlit Orchard / Moonlit Rooftops / Crystal Cave) with multi-layer parallax backgrounds
- Player with 8-frame run cycle, blinking idle, jump poses, star-power variants
- Enemies (per-world recolored beetles, stompable), spinning gems, pulsing power star, waving flag
- Custom 5×7 pixel font, C64-family 16-color palette, C64-style overlay windows
- Authentic C64 SID emulation in `audio.js` (3 voices + bass noise, pulse/sweep/triangle/LFSR-noise,
  ADSR, filter table, controllable vibrato, 3-note arpeggios, *"Chrome Circuit"* loop + 7 SFX)
- Game runs fully silent and playable if audio is unavailable (`window.__SID` guarded)

## Files

- `index.html` — the entire game (inline JS, loads `audio.js` first)
- `audio.js` — self-contained SID chiptune engine (`window.__SID` API)
- `composition.json` — Qwen's *"Chrome Circuit"* note notation (source data for the music)
- `CHANGELOG.md` — full development history (v1.0 → v1.6)
