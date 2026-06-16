# NEON SWARM — Visual Elite Pass (Frontend only)

## Source
Single self-contained file: /app/neon_swarm_ultimate_super_amazing_no_assets.html
(served copy mirrored to /app/index.html via `python3 -m http.server 3000`)

## Goal
Match the reference start-screen and elevate the whole game's UI with sleek
sci-fi motion, without breaking gameplay logic.

## Implemented (2026-06-16)
- Outer HUD corner-bracket frame on all panels (cyan top / magenta bottom), injected via JS.
- Perspective neon grid floor inside #menu (auto-hidden in gameplay).
- Chrome brushed-metal title with scanlines + travelling shine (removed old rainbow hue-cycle).
- Metallic beveled ENGAGE/UPGRADES/etc buttons with travelling sheen + inner bevels.
- Staggered cinematic entrance of menu contents; subtitle ◄── ──► brackets.
- POPUP DEPLOY: bright centre line draws → flash → panel unfolds from the line.
  Driven by Web Animations API (playDeploy) + decorative .ns-deploy/.ns-deploy-flash,
  re-triggered per open via a MutationObserver. Applies to shop, settings, game over,
  pause, cause/effect, first-person prompts.
- Lighter popup backdrop (blur 3px, rgba(2,5,14,.46)) — fixed "dark & blurry" complaint.
- In-game HUD polish (score/wave glow pulse, angular currency box, XP bar shimmer).
- Punchier, non-generic copy (settings, first-person, orientation, cause-effect).

## Verified via screenshots (no console errors)
Menu, Settings, Shop/Armory, Pause — all render correctly; panels reach opacity 1 /
transform none after deploy; grid floor does not overlay gameplay; HUD does not block playfield.

## Notes
- All changes are appended/authoritative CSS + one decor IIFE near </body>; core game JS untouched.
- Backend/MongoDB not used (static HTML game).

## Backlog / Next
- Optional: apply deploy reveal to the orientation/flip overlay.
- Optional: sound cue synced to the deploy flash.
- Optional: shareable score card on Game Over for virality.

## Update (2026-06-16, pass 2)
- Replaced scaleY "unfold" with 3D rotateX FOLD-OUT on open + FOLD-IN on close (WAAPI in playOpen/playClose; close detected via inline opacity='0').
- Removed dark/opaque backdrops on shop/settings/pause/gameover/prompts (transparent bg + backdrop:none). Pause vignette transparent. orientationOverlay keeps its dark.
- PERF: removed always-on full-screen animations (ambientPulse/ultraAuroraDrift/neonGridDrift). Added html.ns-ingame class (toggled by watching #hud) that hides html::before/after + body::before/after during gameplay for FPS.
- PHYSICS: title split into per-letter .ns-letter spans with staggered 3D spring entrance; continuous gradient preserved via per-letter background-size/position. Springy button press on all buttons (pointerdown squash -> overshoot release).
- FIRST PERSON glide: updateFirstPersonMovement now uses velocity momentum (accel into input, coast on release, frame-rate-independent smoothing) + smoothed yaw rate (firstPersonVelX/Y, firstPersonYawRate). Reset in activate/end.
- Verified: menu, settings(open+close), shop, in-game pause — all fold correctly, transparent backdrops, gradients intact, no console errors.
