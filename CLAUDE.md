# Project context for Claude

A single-page public-facing joke fan site — a "tactical briefing" for securing Justin Bieber tour tickets, framed as a classified document operated by four autonomous AI agents. Born out of testing Anthropic's [Claude Design](https://claude.ai/design) handoff workflow, then implemented here via Claude Code.

## Status: shipped

- **Repo:** https://github.com/katehostetler/operation-bieber-fever-2026 (public)
- **Live:** https://katehostetler.github.io/operation-bieber-fever-2026/
- **Hosting:** GitHub Pages, served from `main` branch, root path.
- **Analytics:** none yet. Kate was offered GoatCounter + needs to sign up and paste a tracking code if she wants visitor stats.

## File map

- `index.html` — the site (also serves as the Pages entry).
- `operation-ticket-drop.html` — byte-for-byte duplicate of `index.html`. Kept because Kate's earlier delete was hook-blocked; safe to remove on future cleanup if she's fine with it.
- `README.md` — public-facing joke README (clinical Bieber-fever framing + Rationale + Provenance).
- `.gitignore` — excludes `.claude/`, `.DS_Store`, `*.log`, `node_modules/`.
- `.claude/settings.local.json` — local harness settings, gitignored.

## Key design choices

- **Fonts:** Fraunces (serif, variable with WONK + SOFT axes) + JetBrains Mono.
- **Palette:** pink `#f5c3cd` background, ink `#0e0e10`, accent red `#c8352e` for critical states.
- **Font handoff:** the original design system flagged Helvetica Neue → Inter Tight as a substitute. This standalone page uses Fraunces instead (editorial serif vibe).
- **Dark mode:** toggle in the bottom-right mini tweaks panel. Preference persists via `localStorage`, defaults to OS `prefers-color-scheme`.

## Transmission intro (immersive YouTube overlay)

Full-viewport video intro with `https://www.youtube.com/watch?v=VkbT0a0VW7c`. Key implementation notes:

- **MUST be served over HTTP (not `file://`)** for the YouTube IFrame API to work — origin handshake fails on `null` origin.
- Player is **constructed programmatically** via `new YT.Player(...)` with `host: 'https://www.youtube.com'` + `origin: window.location.origin` — pre-rendered iframes without an origin param have their `postMessage` commands silently ignored.
- **Loop is handled manually** via `onStateChange → ENDED → seekTo(0) + playVideo()`, NOT via YT's `loop=1&playlist=<id>` playerVars. The built-in loop re-reads playerVars every cycle and re-applies `mute=1`, which kills user audio preference.
- **Audio watchdog:** a 400ms `setInterval` enforces `userWantsSound` vs live `player.isMuted()`. Handles any race where YT silently re-mutes. Only runs while the overlay is open and user has unmuted.
- **Enter Briefing → mini-player mode** (not a dismiss): video shrinks to a 260–360px frame pinned bottom-right, keeps playing, page scroll unlocks. Click frame to expand, × to fully dismiss, Skip fully dismisses. `Replay Transmission` handle returns after full dismiss.
- **Pulsing border:** CSS keyframes at ~112 BPM (2143ms per 4-beat bar) drive `box-shadow` on `.xm__frame` plus `scale` on the pink corner brackets. Not tied to real audio — YT iframe is cross-origin so Web Audio API can't read it. Faked tempo-based pulse.

## Key interactive features

- Live countdown to next Friday 10:00 AM PT.
- Interactive `§ 05 Pre-Flight Checklist` with per-group progress counter.
- Risk Register `§ 04` — 8 rows, likelihood × impact pills. Current hard price ceiling: **$5,000** per seat (was $850 GA in earlier drafts — Kate updated).
- Decision tree SVG `§ 03` — SF → Chicago → Austin → Resale → Signal Fire cascade.
- Agent roster `§ 02` — kidrauhl / JB / Oscar / Piggy.

## Running locally

```sh
cd /Users/katehostetler/projects/scratch/jb-tour
python3 -m http.server 5173
open -a "Google Chrome" "http://127.0.0.1:5173/"
```

Do **not** open via `file://` — the video intro will fail.

## Verification / deploy loop

```sh
# After editing index.html, sync the duplicate:
cp index.html operation-ticket-drop.html
# Commit + push:
git add index.html operation-ticket-drop.html && git commit -m "..." && git push
# Check Pages build (typically ~30-60s):
gh api repos/katehostetler/operation-bieber-fever-2026/pages/builds/latest --jq '.status'
# Verify live:
curl -s -o /dev/null -w "%{http_code}\n" https://katehostetler.github.io/operation-bieber-fever-2026/
```

## Known gotchas

- Pages rename has a brief CDN propagation lag (~30-60s). Old repo URL redirects via GitHub.
- GitHub Pages on a free account requires a **public** repo. This one is public — Kate approved after the fact.
- GitHub doesn't provide visitor analytics for the live Pages site, only repo traffic (which doesn't count owner views).
