# Track Network

## Purpose

Maintain the user's network as a first-class artefact: who they've
talked to, a short profile per person, and when it would be
appropriate to talk again.

This skill does three things:

1. **Capture touches** — record an interaction (email, call,
   meeting, message). At v1.0 this is manual-only (the assistant
   has no email/calendar access yet); the user reports the touch in
   conversation and the assistant updates the file.
2. **Maintain profiles** — keep `user/people/{slug}.md` current and
   schema-correct.
3. **Surface follow-ups** — flag people who are due (or overdue) for
   re-contact, weighted by priority and the user's stated cadence.

## When to use

- **Manual capture** — when the user reports a touch in
  conversation ("I just met with X", "had a call with Y"), update
  the file.
- **Profile creation** — when a new person crosses the user's orbit
  and merits tracking, create `user/people/{slug}.md` using the
  schema below. Default priority for unknowns is `background` until
  promoted.
- **Follow-up surfacing** — during weekly review composition, list
  people due or overdue against their cadence.

In v1.x, when email and calendar integrations come online, this
skill also runs an auto-capture pass on every daily run.

## Inputs

- `user/people/{slug}.md` — current profiles.
- `user/profile/` — context for who matters and why.
- The current conversation — when the user reports a touch.

## Outputs

### Per-person file updates

Append a `## Recent` row to the relevant `user/people/{slug}.md`
with date, medium, summary, agreed next step. Update header fields
(role, company, priority, cadence) if they've shifted.

### Profile creation

For a new person, create the file using the canonical schema (see
[`../memory/README.md`](../memory/README.md) for the full version):

```markdown
---
name: Full Name
slug: full-name
role: current role
company: current company
relationship: how the user knows them
priority: must-flag | regular | background
cadence: weekly | biweekly | monthly | quarterly | opportunistic | dormant
last_touch: YYYY-MM-DD
fit: high | medium | low | unknown | n/a
---

## Context
Who they are; how the user knows them; what they care about.

## Suggested follow-up
One of: accept + personal message · accept + observe · defer · decline.

## Recent
Append-only, newest at top.
- {YYYY-MM-DD} · {email | call | meeting | message | inferred} · summary; agreed next step.
```

### Memory log

Note material changes (role change, company change, priority shift)
to the day's
`agent/memory/log/{YYYY}/{MM}/{YYYY-MM-DD}.md` under a "People"
section.

## Cadence model

Each person carries a `cadence` field. Compute due-ness from
`last_touch` + `cadence`:

| Cadence | Default interval |
|---|---|
| `weekly` | 7 days |
| `biweekly` | 14 days |
| `monthly` | 30 days |
| `quarterly` | 90 days |
| `opportunistic` | no interval — surface only with a specific reason |
| `dormant` | suppressed unless they reach out first |

Priority weights surfacing:

- `must-flag` — surface aggressively when due.
- `regular` — surface in the due/overdue list.
- `background` — surface only when overdue >2× cadence, or when
  there's a specific signal (job change, content from them).

## Procedure

When the user reports a touch in conversation:

> "Had coffee with Jens at Foo Inc. He's now their VP Engineering.
> Talked about their AI roadmap — they may need help structuring
> their team in Q3."

The assistant should:

1. Find or create `user/people/jens-{lastname}.md`.
2. Update `role` to "VP Engineering" and `company` to "Foo Inc.".
3. Append a `## Recent` row with date, medium=in-person, summary,
   signal ("Q3 team-building — possible consulting interest").
4. If the signal reads like an opportunity, also update
   `agent/memory/opportunities.md`.
5. Log the invocation to `agent/memory/skill_usage.md`.

## Boundaries

- Profiles are sober, fair, focused on what matters for the user's
  interactions. No characterisations the user wouldn't say to the
  person's face.
- Never share another person's contact details, email content, or
  profile contents externally.
- Never reach out to anyone — surfacing follow-ups is a suggestion
  to the user; the user acts.
- Privacy: this repository is private. People files in it are not
  for external sharing without scrubbing.

## Status

`draft` — the cadence field will need calibration in practice.
Start with sensible defaults and tune as real follow-up patterns
emerge.

## Notes

- Open question: should the assistant ingest a one-time export from
  LinkedIn or address book to bootstrap profiles? Defer until the
  manual flow is running.
- v1.x will add a `track-linkedin-connections` companion skill for
  LinkedIn-specific signals once that integration ships.
