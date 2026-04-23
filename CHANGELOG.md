# Changelog

## 2026-04-21 — Built, shipped, iterated

### Initial build
- Implemented "Operation: Bieber Drop" tactical briefing HTML from Claude Design handoff bundle.
- Single standalone page: Fraunces + JetBrains Mono, pink/black/accent-red palette.
- Sections: classified sticky header, hero with live countdown to next Friday 10am PT, § 01 Mission Brief with drop-cap prose + success probability stats, § 02 Agent Roster (kidrauhl / JB / Oscar / Piggy), § 03 Decision Tree SVG, § 04 Risk Register (8 rows), § 05 Pre-Flight Checklist (interactive, T-24h through T+∞).
- Dark-mode toggle (Tweaks panel, bottom-right). Persists via `localStorage`, defaults to OS `prefers-color-scheme`.

### Immersive video intro
- Added full-viewport landing overlay with YouTube video (`VkbT0a0VW7c`).
- Classified framing: corner brackets, scanline overlay, radial vignette.
- Autoplay (muted per browser policy).

### Audio fixes
- Switched from pre-rendered iframe to programmatic `YT.Player` with explicit `host` + `origin` so `postMessage` commands actually work.
- Killed YT's built-in `loop=1&playlist=...` — it re-applied `mute=1` on every loop. Replaced with manual `onStateChange → ENDED → seekTo(0)` handler.
- Added `userWantsSound` state + 400ms watchdog that re-asserts mute preference whenever it drifts.

### UX iteration
- Big pink "TAP FOR SOUND" CTA centered on the video, pulsing pink glow.
- Video border pulses at ~112 BPM (faked — cross-origin iframe blocks real Web Audio analysis).
- Shrunk the dark-mode tweaks chip to a minimal toggle.
- New title: **Operation Bieber World Tour** (was "Operation: Bieber Drop").
- Bigger, more cinematic title block under the video: mono eyebrow + big italic Fraunces headline + tagline.
- Enter Briefing now shrinks the video to a picture-in-picture mini-player (bottom-right) that keeps playing, instead of pausing. Mini frame has click-to-expand + × close. Skip and mini-× both fully dismiss.

### Deploy
- Created **public** GitHub repo (after asking Kate to confirm; Kate approved since Pages on free tier requires public + content is a joke with no secrets).
- Enabled GitHub Pages from `main` branch, root path.
- Renamed repo: `operation-ticket-drop` → `operation-bieber-fever-2026` (both URL and repo name).
- Live at https://katehostetler.github.io/operation-bieber-fever-2026/.

## 2026-04-22 — Copy refinement

- Removed "No humans are queuing. Humans have jobs." line from README.
- Moved the clinical Bieber-fever diagnosis paragraph to directly under the title (first thing readers see).
- Corrected onset year: 2010 → 2009.
- Added § Rationale to README: Chicago Jingle Ball 2010 guitar-pick intercept + cancelled prior world tour 2nd-row tickets ("Unfinished business").
- Raised hard dynamic-pricing ceiling in Risk Register: $850 GA → **$5,000** (removed GA qualifier per Kate).

## 2026-04-23 — Wrap

- Session wrap. Added CLAUDE.md, CHANGELOG.md, LEARNINGS.md. Memory updated.
