# CHANGELOG — Retro Sisters

## v1.7 — Cracktro "RobD0511 AI Crew" (2026-11-19)

- **New intro state `crack`:** the game now boots into a C64-style cracktro before the
  title screen — rainbow-coloured sine scroller ("ROBD0511 AI CREW PRESENTS · RETRO SISTERS · …"),
  animated broken microchip (two drifting chip halves) and a dedicated SID jingle
  (`crackJingle`, music slot 3 in `audio.js`) plus a `crack` sound effect.
- Enter / Space / click / Start button leaves the cracktro to the title screen (`toTitle()`);
  the key press is not passed through to `start()`.
- **Audio toggle:** a small fixed "Audio: ON/OFF" button is shown only during the cracktro.
- **Clean cracktro screen:** game title, control buttons and the complete game manual
  below the canvas (movement controls and gameplay tips) are hidden while `state === 'crack'`
  and reappear unchanged on the title screen (`syncCracktroUI()`).
- Verification: headless Firefox harness — 12 s cracktro without exceptions, scroller
  continuous and right-to-left, SID sequence `startMusic(3) → playSFX(crack) → stopMusic → startMusic(0)`
  correctly timed, state flow `crack → title → play` correct. Final state tested in the
  browser and accepted by the user.
- Game mechanics, levels, physics and the "Chrome Circuit" music are unchanged.


## v1.6 — Final cleanup before GitHub publication (2026-11-15)

- **Codex (workspace-write):** removed the black debug HUD (state/frame/vx/held/err display)
  and all debug-only code: `const debug={...}`, `drawDebugHUD()` and its call sites,
  the `rsload` sessionStorage counter, the debug-only `error`/`unhandledrejection`/`pointerdown`
  listeners, and all `debug.X` counters.
- **Kept intact:** the game-loop protection (try/catch in `frame()` with `acc=0` and
  `ctx.setTransform(1,0,0,1,0,0)`), normal HUD (score/lives/level/STAR), all physics,
  controls, graphics and the Qwen composition „Chrome Circuit“ (`audio.js` md5
  `b874c8ebad89f7711d3df87480ab905d` unchanged).
- Verified: zero remaining `debug`/`drawDebugHUD`/`rsload` identifiers; script brackets
  balanced (1,289 pairs); only `index.html` touched (37,094 -> 35,810 bytes).
- Final version successfully tested in the browser on Zorin OS by the user.

## v1.5 — Grafikberholung by Claude Fable 5.2 (2026-11-15)
- Model verified: `claude --model fable` (alias accepted, exit 0, model self-reports `claude-fable-5-2`), run with `--permission-mode acceptEdits --allowedTools Read,Write,Edit --add-dir` scoped to the project. No paid APIs, no extra balance.
- Fable development round (1 round): `index.html` 20,142 → 37,114 bytes. New pixel art: player with 8-frame run cycle + idle blink + 3 jump poses + star-power/take variants (9-row head/4-row body/3-row legs sprite data), per-world recolored bug with 2 run frames, 4-frame spinning gem, pulsing power star, custom 5×7 pixel font (`ptext`), per-world tilesets (ground/inner/platform/brick, animated `deco` props, star-emblem bonus block, waving heart flag), multi-layer parallax backgrounds per world (Orchard: sun/clouds/birds/snow mountains/tree rows/apple trees; rooftops: twinkling stars/meteor/moon/two skylines with windows and blinking antenna lights; crystal cave: stalactites/crystal clusters/floating dust/glitter + water/mist), new `titleScene()` (striped sun, house on hill, running sisters, wave logo), C64-family 16-color palette `C` + per-world theme colors, overlays as C64-style windows with per-state animation, HUD restyled (all text fields incl. STAR preserved; score/lives/levelname moved next to debug box because they had been unreadable under it before).
- Scope enforcement verified by Hermes: `.backup-v1.4/` snapshot taken before; after: 17/17 protected regions byte-identical (`update/move/solid/tile/frame/load/die/pause/resume`, input listeners, `maps[]`, `T=16 GRAV=880 W=512 H=288`, `__SID` calls, debug HUD fields incl. `vx`/`held`), bracket balance PASS, `audio.js` md5 `b874c8eb…` and `composition.json` md5 `ab805acc…` unchanged.
- Codex technical review (read-only sandbox): ACCEPT — no undeclared function calls, no TDZ/template-literal/canvas-API issues, canvas-stub simulation of render for all 7 states × 3 levels × 6 animation times ran 126 draw calls error-free; flagged per-frame background column loops as non-guaranteed 60 fps (not disqualifying).
- Files changed: `index.html` only. New dir: `.backup-v1.4/` (pre-change snapshot).
- Not practically testable: real browser rendering, animation smoothness, 60 fps performance (no JS runtime/browser on VM).

## v1.4 — Music round: new SID composition "Chrome Circuit" (2026-11-15)
- Complaint: old procedural music was monotonous, nervous, loop repeated too fast (≈16 s procedural track).
- Qwen (via Hermes delegation, real run, 1074 s, model qwen3.8-flash-next-coder-iq1_m): original composition "Chrome Circuit", 32 bars @ 150 bpm, 3 voices (lead/harmony/bass), 4 sections (Statement / Answer & Inversion / High-Register Refrain / Recap & Cadence), 16th-note grid, walking bass runs, arpeggio triples, seamless loop spec → written to `composition.json`.
- Codex (workspace-write, 1 round): implemented composition in `audio.js`: replaced procedural `buildTrack()`/`sequence()` with coded `chromeCircuit` track data; extended engine additively in `trigger()`/`tick()` only: note 0 = rest (silence), `vib:[semitones, period_frames]` semitone-correct vibrato, `preset:"pluck"` bass ADSR; sweep `code:127` on sustained lead notes; all 3 `startMusic` slots use the new song; SFX/API untouched. Duration: 512 slots × 6 frames = 3072 frames = 51.2 s at 60 Hz `tick()` (verified: `tick()` driven by `framePhase += FRAME(60)`, not PAL 50 Hz).
- Claude Code review found: every event had `"vib":[0,15]` → vibrato amplitude 0 → vibrato nowhere (real defect); timing-50Hz concern refuted by Hermes (FRAME=60 accumulator).
- Hermes correction pass (mechanical data transform): lead `vib:[1.5,5]` on the 4 events ≥83 in bars 16/22; harmony `vib:[1,15]` on 104 sustained events (≥12 frames), 1-slot arpeggio runs clean; bass no vibrato; zero disabled `"vib":[0,15]` left. Re-verified: lead/bass events byte-identical to Qwen notation, harmony = Qwen + approved extension bars 29–32, all 3 voices exactly 512 slots / 3072 frames (loop drift 0), bracket balance PASS.
- Files changed: `audio.js` (13,087 → 41,293 bytes). `index.html` UNCHANGED (20,142 bytes). New project files: `composition.json`, `preview_synth.py` + WAV preview in hermes-output.

## v1.3 — Bugfix round 4: horizontal movement (2026-11-14)
- Symptom (Chrome/Zorin, 4th report): game starts, jump works, but no left/right movement.
- Investigation (Codex + independent analysis + Claude review): keyboard chain, key mapping, horizontal velocity, collision, position update ALL verified correct: exactly one `keys` Set (no shadowing), single keydown/keyup listener pair (`keys.add(e.code)` before repeat-guard / `keys.delete(e.code)`), dir from `ArrowLeft/ArrowRight/KeyA/KeyD`, one and only `player.vx` assignment (acceleration line), no per-frame reset; faithful Python port of `solid()`/`move()` + movement code with the REAL maps moves the player x=34→238 px in 2 s. No provable code defect → no speculative fix applied (per policy).
- Jump-vs-run asymmetry identified (Claude): jump is event-driven (`jumpBuffer` set in keydown, survives), run is POLLED (`keys.has` at update time) → the missing ground truth is what the browser actually delivers.
- Change (instrumentation only, HUD extended, all old fields kept): first HUD line now also shows `vx:` (`player?Math.round(player.vx):0`, guarded — `player` is undefined before `load()`) and `held:` (comma-joined contents of the `keys` Set, `-` when empty); HUD bg rect widened 252→336, fillText wrap 248→330.
- Claude Code reviewed the excerpt (HUD safe: `player` in top-level `let` list → ternary guard sufficient, no TDZ; `Array.from(new Set())` safe). Discriminator table: `held:-` while Space shows `Space` → input-side cause; `held:ArrowRight` + `vx:0` → wall-branch/`vx` zeroing; `held:ArrowRight` + `vx:≈105` but no motion → render/camera issue.
- Static tests after change: `()` 419/419, `{}` 130/130, `[]` 40/40 balanced; guard present exactly once, unguarded variant absent; `drawDebugHUD` 1 definition + 2 call sites. `audio.js` untouched (md5 feeb947305ff6bc025404323a1339af9).
- Browser playtest still NOT possible from VM (no JS runtime, headless Firefox exit 139) — read `held:`/`vx:` on Zorin to pinpoint.

## v1.2 — Bugfix: Root cause of frozen start (2026-11-14)
- Symptom (Chrome/Zorin, 3rd report): title OK, music OK, Start/Restart click does nothing, no console error — persisted after v1.1.
- **Root cause (proven, code-level)**: spike/flag check line in `update()` — `for(...)for(let x=...)if(tile(x,y)==='v'){die();return}if(tile(x,y)==='F'){...}`. The flag `if` sits **outside both for-loops**, so `x`/`y` are out of scope there; in strict mode this throws `ReferenceError: x is not defined` on the first `update()` in `play` state. `frame()` aborted **before rescheduling** `requestAnimationFrame` → render loop dead → canvas frozen on the last title frame. Title screen itself never covered the game (overlay draw calls are state-guarded — hypothesis refuted by code read).
- Fix 1: both tile checks moved inside the inner loop body with braced block `{const c=tile(x,y);if(c==='v'){die();return}if(c==='F'){...;return}}`; `return` on flag touch prevents double processing that frame.
- Fix 2 (diagnostics resilience): `frame()` now wraps update+render in try/catch — error text recorded to HUD, `acc=0` (no unbounded accumulator), `ctx.setTransform(1,0,0,1,0,0)` (no leaked player transform into HUD), `requestAnimationFrame` always rescheduled → a throwing frame can no longer kill the loop.
- Fix 3 (debug HUD, kept for Zorin readout, top-right, 2 lines): `state`, `click` (canvas clicks), `btn` (button clicks), `tgt` (pointerdown target id — reveals invisible overlays), `call` (start() invocations), `ok` (starts past guard), `frame` (rAF ticks), `load` (session reload counter via sessionStorage), `err` (captured error or `no err`).
- Claude Code reviewed the diff (ACCEPT): scoping correct, transform reset safe (no base transform at init — verified by grep), acc clamp already present (`Math.min(...,.1)`), no new bugs.
- Tests (static, python3, 14 assertions): all script blocks balanced; scope fix present; catch resilience present; all HUD counters wired; blur listener still absent; audio.js untouched (md5 feeb947305ff6bc025404323a1339af9). Browser playtest NOT possible from VM (no JS runtime, headless Firefox crashes exit 139) — verify on Zorin.
- If HUD ever shows `err:` non-`no err`, the exact message is now readable in-game.

## v1.1 — Bugfix: Start/Restart click (2026-11-14)
- Symptom (Chrome/Zorin): title screen OK, SID music OK, click on Start/Restart does nothing, no console error.
- Root cause: `window.addEventListener('blur',()=>{if(state==='play')pause();keys.clear()})`. In Chrome the first focus move (document → button/canvas, triggered by `start()`'s `canvas.focus()` inside the click handler) fires a window 'blur' event — right after `start()` set `state='play'` — so `pause()` flipped the game to paused before the first frame. Silent, no error.
- Fix (Codex, verified diff = exactly one line): removed the window 'blur' auto-pause listener. Tab-switch pausing remains covered by the `visibilitychange` listener. No new features, nothing else touched; `audio.js` unchanged (md5 feeb947305ff6bc025404323a1339af9).
- Claude Code reviewed the diff twice; blur-ordering nuance incorporated (window-blur quirk fires on the document→element focus move — exactly the path `start()` triggers). Remaining pause paths are user-initiated (P/Esc, pause button) plus tab-hidden.
- Tests (static, python3): JS brace/paren balance PASS; blur listener gone; start/pause/canvas-click/keyboard-start bindings intact; exactly 1 changed line vs. before; audio.js untouched. Browser playtest NOT possible from VM (no display, no JS runtime, headless Firefox crashes) — must be verified in Zorin browser.

## v1.0 (2026-11-14)

### Development (coding-team workflow)
- `audio.js` developed by Codex (workspace-write), reviewed by Claude Code (safe-mode, 9 findings)
- Correction round 1 (audio.js): re-init guard, envelope-rate lookup, AudioContext ctor, voice deactivation on closed gate, `ready` getter, track-range check, autoplay-policy unlock
- `index.html` developed by Codex, reviewed by Claude Code (12 findings)
- Correction round 1 (index.html): keydown repeat-order fix (held keys survive pause/respawn, no keys.clear), start() state guard, local SFX gate, vertical-collision direction captured before loop, brick-break sound, spikes made lethal, map validation, sprite flip centering, guarded button binding with blur() (buttons no longer steal Space/Enter)

### Verification
- Static checks: braces/parens/brackets balanced, all `window.__SID` API names present, audio.js loaded before game script, no fetch/external URLs, 3 levels 18×96 with exactly one spawn + one flag each — PASS
- Automated playtesting impossible in this VM (no JS runtime, no C compiler for user-level builds, no display for Firefox) — playtest on the user's Zorin browser pending
