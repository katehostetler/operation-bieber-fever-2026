# Operation Bieber World Tour

A clinical response to an incurable diagnosis of Bieber fever, first presenting in 2009 and periodically flaring whenever a tour is announced. Symptoms include, but are not limited to: involuntary Ticketmaster refreshes, elevated heart rate during "One Less Lonely Girl," and the unshakeable belief that this time, the front row is attainable.

## Rationale

The subject's belief is not irrational. Prior evidence supports the operating hypothesis that close proximity is attainable:

- **Chicago Jingle Ball, 2010.** Subject held a second-row seat. Justin Bieber, unprompted, threw his guitar pick into the crowd. Subject caught it.
- **Most recent world tour.** Subject secured second-row tickets during general onsale. Tour was cancelled before the seats could be used. Unfinished business.

Future onsales are therefore treated as a continuation of prior engagement — not speculation.

There is no known treatment. The briefing document is a coping mechanism.

> This document is for hypothetical operational planning only. (and was also created solely to test the new Claude Design feature and likely will never be looked at again).

## Live

**→ [katehostetler.github.io/operation-bieber-fever-2026](https://katehostetler.github.io/operation-bieber-fever-2026/)**

Features a countdown to the next Friday 10:00 AM PT, an interactive pre-flight checklist, a classified-style video transmission with a border that pulses in time to the beat, and a dark-mode toggle.

## Provenance

A test of Anthropic's new [Claude Design](https://claude.ai/design) tool — a design mocking environment where you iterate on HTML/CSS/JS prototypes with an AI, then export a handoff bundle for a coding agent (in this case, [Claude Code](https://claude.com/claude-code)) to implement for real.

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
