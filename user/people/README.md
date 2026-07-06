# People — your network

One file per person you interact with or that the assistant needs
context on for triage and digest composition. Lives under `user/`
because the network is personal to you, not part of the assistant's
curated knowledge layer.

File naming: `{firstname-lastname}.md` (lowercase, hyphenated). For
ambiguous names, append a disambiguator (e.g. `jens-hansen-bo.md`).

## Schema

The canonical schema for a person file is documented in
[`../../agent/memory/README.md`](../../agent/memory/README.md#peopleslugmd).
A short version:

```markdown
---
name: Full Name
slug: full-name
role: current role
company: current company
relationship: how you know them
priority: must-flag | regular | background
cadence: weekly | biweekly | monthly | quarterly | opportunistic | dormant
last_touch: YYYY-MM-DD
fit: high | medium | low | unknown | n/a
# Optional contact channels:
email: preferred@example.com
linkedin: handle-or-url
---

## Context
Who they are; how you know them; what they care about.

## Suggested follow-up
One of: accept + personal message · accept + observe · defer · decline.

## Recent
Append-only, newest at top.
- {YYYY-MM-DD} · {email | call | meeting | message | inferred} · summary; agreed next step.
```

## Cadence model

The `cadence` field drives "due for re-contact" surfacing in the
daily digest:

| Cadence | Default interval |
|---|---|
| `weekly` | 7 days |
| `biweekly` | 14 days |
| `monthly` | 30 days |
| `quarterly` | 90 days |
| `opportunistic` | no interval — surface only with a specific reason |
| `dormant` | suppressed unless they reach out |

## Privacy

The assistant writes notes about other people here. Treat each entry
the way a private note would be treated: accurate, fair, focused on
what matters for *your* interaction with them. The assistant follows
the same posture.

This repository is private to you. Keep it that way — or scrub
people files before sharing any part of the repo externally.

## Maintained by

The [`agent/skills/track-network.md`](../../agent/skills/track-network.md)
skill keeps these files current — captures touches, updates header
fields, surfaces follow-ups.
