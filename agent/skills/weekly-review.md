# Weekly Review

## Purpose

End-of-week recap and week-ahead framing. Slower and more
reflective than a normal session. Reads the week's accumulated
material and produces a structured digest with one section per
theme that matters.

## When to use

- Once per week. Default day: Sunday morning, in the user's
  timezone (confirm with them on first use).
- On demand when the user asks for a weekly review explicitly.

At v1.0 the routine isn't running on a schedule yet — the user
invokes it manually. Once the scheduler ships in v1.x, this skill
runs automatically per the user's `agent/routines.md` opt-in.

## Inputs

- Past week's `agent/memory/log/{YYYY}/{MM}/` entries.
- `agent/memory/opportunities.md`.
- `agent/memory/decisions.md`.
- `agent/memory/observations.md`.
- `user/profile/goals.md` (30-day and 90-day targets).
- `user/people/` — for the network-movements section.
- Past week's `user/tasks/` — what shipped, what's still in flight.

## Outputs

`user/digests/{YYYY}/{MM}/{YYYY-MM-DD}-weekly.md` containing the
weekly digest.

Plus:

- Updates to `agent/memory/observations.md` (patterns from the
  week).
- A refreshed `CLAUDE.md` via
  [`sync-claude-md`](sync-claude-md.md) — runs once per weekly
  cycle so the orientation file stays accurate for future sessions.
- An invocation row in `agent/memory/skill_usage.md`.
- A cleanup pass on `agent/memory/short-term-memory/<channel>/`
  per the
  [`short-term-memory`](short-term-memory.md) cleanup window.

## Sections of a weekly digest

The default shape:

1. **Week in review** — what mattered, what was acted on, what was
   missed.
2. **Goal pulse** — progress against 90-day and 30-day targets.
3. **Network movements** — who reached out, who went quiet, who
   changed roles.
4. **Open threads** — opportunities in flight, decisions pending.
5. **Week ahead** — calendar shape, key prep items, focus
   suggestion.
6. **Project orientation refresh** — one line summarising what
   `sync-claude-md` changed in `CLAUDE.md` this week (or "no
   material change").
7. **Assistant note** — sharper, more opinionated than the daily
   exchange. The persona's voice gets more room here.

## Procedure

1. Read the last 7 days of `agent/memory/log/` entries.
2. Read `agent/memory/opportunities.md`, `decisions.md`,
   `observations.md` — note what's new or shifted.
3. Read `user/profile/goals.md` — score progress against the
   30-day and 90-day targets.
4. Read this week's `user/people/` recent rows — surface anyone who
   reached out, anyone who went quiet, anyone who changed roles.
5. Compose each section. Keep it tight — a weekly digest that
   takes 30 minutes to read is one that never gets read.
6. Invoke [`sync-claude-md`](sync-claude-md.md) and note the result
   in section 6.
7. Invoke the short-term-memory cleanup and note the count of
   deleted session files (if any) in the week-in-review section.
8. Write the digest to
   `user/digests/{YYYY}/{MM}/{YYYY-MM-DD}-weekly.md`.
9. Log the invocation to `agent/memory/skill_usage.md`.

## Boundaries

- Same as every other skill: read-only on every external system.
  The weekly digest is a written artefact, not actions taken.
- If the week was thin, say so. Don't pad to look productive.
- Persona voice carries through the digest. The assistant note in
  section 7 is the most opinionated section by design — let the
  voice show.

## Status

`draft`

## Notes

- Day-of-week default (Sunday) is editable in
  `agent/routines.md` once the scheduler ships.
- Once integrations come online (v1.x), this skill grows to include
  the week's mail and calendar passes. The shape stays the same;
  the data sources widen.
