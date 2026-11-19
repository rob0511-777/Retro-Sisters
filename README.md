# Retro Sisters

A complete, original 2D retro jump'n'run game in the style of classic C64 platformers — built as a **multi-agent AI experiment** coordinated by Hermes.

100 % original: custom procedural pixel art, custom level maps, custom SID-style music.
**No** Giana Sisters or other copyrighted material, sprites or level maps.

## Run it (Zorin / any Linux)

Open `index.html` directly in your browser:

    firefox index.html

or via a local-only preview server (nothing publicly reachable):

    python3 -m http.server 8000

No build step, no external libraries, no network access needed.

## Cracktro

The game boots into a C64-style cracktro by the **RobD0511 AI Crew**:

- rainbow sine scroller with the crew's greetings
- animated broken microchip
- dedicated SID cracktro jingle and "crack" sound effect
- "Audio: ON/OFF" toggle (top right, cracktro only)

During the cracktro the page shows only the canvas — title, buttons and game manual are hidden.
Press **Enter / Space**, click the canvas or the Start button to continue to the title screen.

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
- **Claude Code** — independent reviews of game logic, music and code; cracktro verification and finishing
- **Claude Fable 5.2** — the graphical overhaul (pixel art, animations, parallax backgrounds, C64 palette)

The final version, including the cracktro, was **successfully tested in the browser** by the user.

## Features

- C64-style cracktro (sine scroller, broken microchip, SID jingle, audio toggle)
- Tile-based world, 16 px logical tiles, 60 fps fixed-timestep physics, AABB collisions
- 3 themed levels (Sunlit Orchard / Moonlit Rooftops / Crystal Cave) with multi-layer parallax backgrounds
- Player with 8-frame run cycle, blinking idle, jump poses, star-power variants
- Enemies (per-world recolored beetles, stompable), spinning gems, pulsing power star, waving flag
- Custom 5×7 pixel font, C64-family 16-color palette, C64-style overlay windows
- Authentic C64 SID emulation in `audio.js` (3 voices + bass noise, pulse/sweep/triangle/LFSR-noise,
  ADSR, filter table, controllable vibrato, 3-note arpeggios, *"Chrome Circuit"* loop, cracktro jingle + SFX)
- Game runs fully silent and playable if audio is unavailable (`window.__SID` guarded)

## Files

- `index.html` — the entire game incl. cracktro (inline JS, loads `audio.js` first)
- `audio.js` — self-contained SID chiptune engine (`window.__SID` API)
- `composition.json` — Qwen's *"Chrome Circuit"* note notation (source data for the music)
- `CHANGELOG.md` — full development history (v1.0 → v1.7)

## Deutsch

**Retro Sisters** ist ein vollständig originales 2D-Jump'n'Run im Stil klassischer C64-Plattformer,
entstanden als **Multi-Agenten-KI-Experiment** unter Koordination von Hermes. Eigene Pixelgrafik,
eigene Levels, eigene SID-Musik — keine fremden, urheberrechtlich geschützten Inhalte.

- **Starten:** `index.html` im Browser öffnen — kein Build, keine Bibliotheken, kein Netzwerk nötig.
- **Cracktro:** Beim Start erscheint das Cracktro der **RobD0511 AI Crew** mit Laufschrift,
  zerbrochenem Mikrochip, eigenem SID-Jingle und Audio-Schalter. Die Spielanleitung ist dabei
  ausgeblendet. Enter, Leertaste oder Klick führen zum Titelbildschirm.
- **Steuerung:** Laufen A/D bzw. ←/→ · Springen Leertaste/W/↑ · Pause P/Esc ·
  Musik/SFX über die Buttons unter der Spielfläche.
- **Ziel:** Käfer zertreten, gestreifte Blöcke von unten zerschlagen, rosa Sterne für Tempo und
  Unverwundbarkeit einsammeln, Edelsteine sammeln und alle drei Flaggen erreichen.
