# Operation: Bieber Drop

A tactical briefing document prepared by four autonomous agents in advance of the SWAG III US Tour onsale window.

> This document is for operational planning only. It does not constitute a guarantee of outcome.

## Live

**→ [katehostetler.github.io/operation-ticket-drop](https://katehostetler.github.io/operation-ticket-drop/)**

Features a countdown to the next Friday 10:00 AM PT, an interactive pre-flight checklist, a classified-style video transmission with a border that pulses in time to the beat, and a dark-mode toggle. No humans are queuing. Humans have jobs.

## Provenance

This was produced, in full seriousness, as:

1. A test of Anthropic's new [Claude Design](https://claude.ai/design) tool — a design mocking environment where you iterate on HTML/CSS/JS prototypes with an AI, then export a handoff bundle for a coding agent (in this case, [Claude Code](https://claude.com/claude-code)) to implement for real.
2. A clinical response to an incurable diagnosis of Bieber fever, first presenting in 2010 and periodically flaring whenever a tour is announced. Symptoms include, but are not limited to: involuntary Ticketmaster refreshes, elevated heart rate during "One Less Lonely Girl," and the unshakeable belief that this time, the front row is attainable.

There is no known treatment. The briefing document is a coping mechanism.

## Local preview

```sh
python3 -m http.server 5173
open http://127.0.0.1:5173/
```

Must be served over HTTP (not `file://`) — the YouTube IFrame API needs a valid origin for its `postMessage` handshake.

## Credits

- Design: handoff from [Claude Design](https://claude.ai/design)
- Implementation: [Claude Code](https://claude.com/claude-code)
- Fonts: Fraunces + JetBrains Mono (Google Fonts)
- Subject: Biebs
- Affliction: chronic
