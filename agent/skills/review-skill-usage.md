# Review Skill Usage

## Purpose

Validate that the skill set the assistant has is the right one.
Surface skills that aren't earning their keep, gaps that keep
recurring, and skills that should be sharpened.

## When to use

- Once per month — default first weekly review of the month.
- On demand when the user asks for a skill audit.

## Inputs

- [`../memory/skill_usage.md`](../memory/skill_usage.md) —
  invocations and gaps for the period.
- [`README.md`](README.md) — current skill roster and statuses.
- [`../memory/observations.md`](../memory/observations.md) —
  patterns the assistant has noticed.

## Outputs

A review section appended to `agent/memory/observations.md`
covering:

- **Top-used skills** — what the assistant leaned on, frequency,
  and whether output was acted on.
- **Unused or under-used skills** — candidates for retirement or
  refactoring.
- **Recurring gaps** — patterns in `Gaps observed` that warrant
  new skills.
- **Quality flags** — invocations that errored or produced
  low-signal output.

If a clear decision emerges (retire X, add Y), draft an entry for
`agent/memory/decisions.md` for the user to confirm.

Plus an invocation row in `skill_usage.md` (yes — even this skill
logs itself; consistency is the point).

## Procedure

1. Read the period's invocation rows from `skill_usage.md`. Bucket
   by skill, by trigger, by outcome.
2. Read the period's gap entries. Cluster by theme.
3. Cross-reference with `agent/memory/observations.md` — has the
   user reacted to particular outputs? Which skills produced output
   that landed and which didn't?
4. Score each existing skill:
    - **Earning its keep** — used regularly, output landed.
    - **Underused** — invoked rarely; consider retirement or merge.
    - **Failing** — invoked but consistently producing low-signal
      output or errors.
5. For gaps with ≥3 observations in the period, propose a new
   skill: name, purpose, when-to-use, inputs/outputs.
6. Write the review section to `observations.md`.
7. If proposals are clear-cut, draft a decision entry to
   `decisions.md` for the user's review.

## Boundaries

- This skill produces **proposals**, not changes. Skill files are
  not added, removed, or status-changed without the user's go-ahead.
- The decision entry is a draft for the user to confirm — it does
  not get committed to `decisions.md` until the user signs off in
  conversation.

## Status

`draft`

## Notes

- This is the closest the assistant has to a self-improvement
  mechanism in v1.0. Used honestly, it surfaces the difference
  between "skills I have" and "skills I actually use" — which is
  the difference between a useful capability roster and a list.
- Don't be precious about retiring skills that look elegant but
  aren't getting used. A small set of well-used skills beats a
  large set of well-meaning ones.
