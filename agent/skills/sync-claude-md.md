# Sync CLAUDE.md

## Purpose

Keep `CLAUDE.md` accurate without the user hand-editing it. Refresh
the *Current state* paragraph and the *History* list so future
sessions loading the repo get an honest picture in their
auto-loaded context.

`CLAUDE.md` is the highest-leverage piece of context in the
repository — every session reads it before doing anything else.
Drift here means every future session starts from a slightly wrong
understanding.

## When to use

- **Weekly**, as part of [`weekly-review`](weekly-review.md).
- **On demand** when the user asks for a refresh or notices
  staleness.
- **Triggered by a load-bearing decision** — if a decision in the
  current session reshapes how the project should be described,
  bump `CLAUDE.md` immediately rather than waiting for the weekly
  pass.

## Inputs

- Current `CLAUDE.md`.
- `agent/memory/decisions.md` — for entries since the last refresh.
- `user/profile/situation.md`, `user/profile/goals.md` — for
  principal-level state changes.
- `agent/memory/opportunities.md` — for active pipeline.
- `agent/skills/README.md` — for the current skill roster.

## Outputs

Edited `CLAUDE.md`:

- The *Current state* paragraph replaced between the markers
  `<!-- sync-claude-md:current-state-begin -->` and
  `<!-- sync-claude-md:current-state-end -->`.
- The *History* bullet list replaced between
  `<!-- sync-claude-md:history-begin -->` and
  `<!-- sync-claude-md:history-end -->`.
- The `_Last refreshed: YYYY-MM-DD._` line at the top of *Current
  state* updated.

Plus a one-line entry in the weekly review noting what changed
(e.g. "CLAUDE.md refreshed: added 2026-06-15 decision on X;
rewrote current-state paragraph after Tuesday's meeting").

Plus an invocation row in `agent/memory/skill_usage.md`.

## Procedure

1. Read `CLAUDE.md`.
2. Parse the `_Last refreshed:_` date inside the *Current state*
   block.
3. Read `agent/memory/decisions.md`; collect every entry dated after
   the last refresh.
4. Read `user/profile/situation.md` and `user/profile/goals.md`.
   Diff the high-level facts against what *Current state* in
   `CLAUDE.md` asserts. Examples of things that flip and need
   reflecting:
    - Current role / employment state
    - Active opportunity pipeline composition
    - Stated goals or priorities
    - Voice or boundaries changes
5. Read `agent/skills/README.md`. If the skill roster has changed
   (new skills authored, skills retired), update.
6. Compose the new *Current state* paragraph. Keep it to 3–5 short
   paragraphs. Don't pad. If the project state is roughly the same
   as last week, the new paragraph can be ~80% the same as the old
   — just bump the date.
7. Compose the new *History* block. Add one bullet per material
   decision since last refresh; keep the structure
   `- **YYYY-MM-DD** — Short one-line summary`. Demote older
   entries off the list if it grows beyond ~10 items (the canonical
   record lives in `agent/memory/decisions.md`, not here).
8. Write the new `CLAUDE.md` by replacing only the two
   marker-bounded blocks.
9. Note the change in the weekly review (or in today's exchange if
   invoked mid-week).
10. Log the invocation to `agent/memory/skill_usage.md`.

## What this skill does NOT do

- Does not touch any section of `CLAUDE.md` outside the two marker
  blocks. The structure of the file (table, load-bearing facts,
  etc.) is hand-maintained by the user.
- Does not edit `user/profile/`, `agent/memory/decisions.md`, or
  any canonical source. Those drive `CLAUDE.md`, not the other way
  around.
- Does not add new sections to `CLAUDE.md`. If a new section is
  genuinely warranted, surface it as a proposal in the weekly
  review and let the user decide.

## Boundaries

- **Self-correcting drift is OK; restructuring is not.** Applying
  small fixes to the two marker blocks is the entire remit.
- **Be conservative with the date.** If nothing material changed
  since last refresh, still bump the date — it signals to future
  sessions that the file was actually checked, not just left to
  rot.

## Status

`draft`

## Notes

- The two marker pairs are HTML comments, invisible in rendered
  markdown. They exist so the skill can find replaceable regions
  reliably.
- If the markers go missing (the user edits the file manually and
  strips them), the skill should refuse to overwrite and surface a
  warning rather than guess where the blocks were.
