# Learnings

## YouTube IFrame API requires a non-null origin

**Symptom:** Video "erroring" or just sitting inert when opened via `file://`.
**Cause:** YouTube's `enablejsapi=1` handshake fails when the page origin is `null` (i.e. loaded from disk).
**Fix:** Always serve via `http(s)`. For local preview: `python3 -m http.server 5173` then open `http://127.0.0.1:5173/`.
**Rule:** Any embed that uses `postMessage` for control (YouTube, Vimeo, etc.) needs a real origin. Never open such pages from the filesystem during development.

## YouTube IFrame API: pass `host` + `origin` explicitly when controlling via JS

**Symptom:** `player.unMute()` / `player.setVolume()` silently no-op even though the iframe is loaded and visible.
**Cause:** Pre-rendering `<iframe src="...?enablejsapi=1">` without an `origin` parameter leaves YouTube unable to verify `postMessage` senders, so it drops control commands.
**Fix:** Construct the player programmatically: `new YT.Player(elementId, { host, videoId, playerVars: { origin: window.location.origin, ... }, events })`.
**Rule:** Always pass `origin: window.location.origin` in `playerVars` when using the JS API.

## YouTube's built-in loop re-applies initial `playerVars` on every cycle

**Symptom:** Audio worked once, then mute came back on the next loop.
**Cause:** `loop=1&playlist=<videoId>` effectively reloads the video, which re-parses `mute=1` from the original playerVars.
**Fix:** Don't use built-in loop. Handle `YT.PlayerState.ENDED` in `onStateChange` and call `seekTo(0, true); playVideo()`.
**Rule:** For looping embeds that need persistent user audio/state, roll the loop manually via the state-change event.

## Autoplay policies are gesture-scoped, not preference-scoped

**Symptom:** Sound would drop mid-playback for reasons not obviously tied to loops.
**Cause:** Browser autoplay policies can silently re-mute when the "user gesture" lineage gets diluted (e.g. programmatic `playVideo()` after long idle).
**Fix:** Track user intent (`userWantsSound` boolean) separately from live state. Run a watchdog interval that re-calls `unMute()` + `setVolume()` whenever live state diverges from intent.
**Rule:** For cross-origin media you can't control directly, always use an intent tracker + enforcement loop rather than trusting one-shot API calls.

## GitHub Pages on free accounts requires a public repo

**Symptom:** "Publishing site to Pages" without thinking about visibility.
**Cause:** Free GitHub accounts can't publish Pages from a private repo. Pro is required, and even on Pro the site itself is publicly accessible unless Enterprise Private Pages.
**Fix:** Either (a) accept a public repo when publishing to Pages, or (b) use a different host (Netlify, Cloudflare Pages, Vercel — all support private sources + public sites on free tiers).
**Rule:** Kate's default is private repos. When Pages is requested, flag the conflict up front and get explicit approval before creating the repo.

## GitHub Pages sites have no built-in visitor analytics

**Symptom:** `gh api repos/.../traffic/views` returns counts that reflect the github.com repo page, not the live Pages site.
**Cause:** GitHub traffic endpoints only instrument github.com itself. Pages visitors are not tracked.
**Fix:** Add client-side analytics to the HTML (GoatCounter, Plausible, Cloudflare Web Analytics if on CF, or GA4).
**Rule:** If a user asks about Pages visitor stats, say so honestly and offer analytics instead of pretending `traffic/views` answers the question.

## Hook-blocked file deletes are a signal, not an error

**Symptom:** `rm operation-ticket-drop.html` was denied mid-session.
**Cause:** The hook flagged it as "deleting a user-referenced file without explicit direction."
**Fix:** Keep both files and sync on every edit (`cp index.html operation-ticket-drop.html`).
**Rule:** When a hook blocks a destructive action, don't work around it — keep the file, adjust the workflow, and flag it to the user.
