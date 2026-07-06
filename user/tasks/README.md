# Tasks — work in flight

Working tray for in-progress drafts, briefs, applications,
speeches, and other ongoing items. Distinct from
[`../digests/`](../digests/) (delivered daily output) and from
[`../../agent/memory/`](../../agent/memory/) (curated facts).

## File naming

`YYYY-MM-DD-slug.md` where the date is the **relevant date for the
item** — the event date, the deadline, the target delivery — not the
creation date.

Example: a wedding speech for 2026-08-12 → `2026-08-12-wedding-speech-jens.md`.

This convention makes the folder lexicographically scannable by
upcoming relevance, not by when the assistant or you first wrote it
down.

## When to write here vs. elsewhere

| If it's… | It goes in… |
|---|---|
| One-off creative or research work in progress | `user/tasks/` (here) |
| Daily-runner output (digest) | `user/digests/` |
| Persistent facts about people | `user/people/` |
| Persistent facts about opportunities, decisions, observations | `agent/memory/` |
| Assistant's configuration | `agent/persona.md` / `agent/boundaries.md` / `agent/routines.md` |

## Lifecycle

When an item is done — speech delivered, brief consumed, role
decided — it can stay as a record or be deleted. The assistant does
not auto-prune this folder.

## What the assistant writes here

When you ask for a draft (an email, a brief, a speech), the
assistant writes the draft as a file in this folder for you to
review. The draft never leaves this repository — the assistant is
read-only on every external system. You send it when you're ready.
