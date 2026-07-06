# Digests

Generated daily and weekly digests. Committed for audit, history,
and pattern review.

## Path conventions

- Daily: `user/digests/{YYYY}/{MM}/{YYYY-MM-DD}.md`
- Weekly: `user/digests/{YYYY}/{MM}/{YYYY-MM-DD}-weekly.md`

## v1.0 status

The daily-digest routine isn't running automatically yet — the
[`agent/routines.md`](../../agent/routines.md) file lists it as
opt-in, but scheduled delivery lands in v1.x. You can ask the
assistant to compose a digest on demand in the meantime; it'll
write the output here as if scheduled, so you get the same shape.

## Composition

The [`agent/skills/weekly-review.md`](../../agent/skills/weekly-review.md)
skill drives the weekly version. The daily version ships when the
routine goes live.

## Why commit history matters

Digests are a record of what mattered, when, and what the assistant
surfaced. A month of digests is a useful artefact in its own right
— a pattern review of "what did the assistant flag, and how often
was it right" is one of the few honest ways to evaluate it.
