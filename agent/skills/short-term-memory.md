# Short-term memory

## Purpose

Carry conversation context across sessions so the next chat doesn't
start cold. Without this, the user opens a fresh conversation
tomorrow and the assistant has no memory of today's drafts, threads,
or work in flight.

The storage lives at
[`../memory/short-term-memory/<channel>/`](../memory/short-term-memory/).
This file is the **discipline contract** — when to read, when to
write, what counts as a session, what to clean up.

## When to use

**Read** at the start of every new session:

- Web CLI session — the assistant reads on its own initiative at the
  start of the session.
- Any future channel — same default: read before responding.

**Write** after every substantive turn:

- Web CLI — the assistant appends the turn after generating a
  response.
- Future channels — channel-managed where possible (a gateway
  pre-loads + auto-writes), assistant-managed where not.

**Clean** weekly, as part of [`weekly-review`](weekly-review.md).

## Inputs

- Session files for the active channel:
  `agent/memory/short-term-memory/<channel>/*.md`.
- The most recent session files from every other channel (when the
  user references content from elsewhere).
- The current conversation turn (from the chat input).

## Outputs

- An append to the active session file — the user's turn, then the
  assistant's response after generation.
- A new session file (`{YYYY-MM-DDTHH-MM-SS}.md`) when the
  inactivity gap exceeds `SESSION_GAP_HOURS`.
- Deletes from the cleanup pass: session files older than
  `CLEANUP_DAYS`.
- An invocation row in `agent/memory/skill_usage.md`.

## Procedure

The procedure has three phases: read at session start, write per
substantive turn, and clean weekly. Each phase is detailed below.

### Reading (session start)

1. At the start of a new session, glob session files for the
   active channel (`agent/memory/short-term-memory/<channel>/*.md`)
   and the most recent file from every other channel.
2. Filter to files with mtime within `LOAD_WINDOW_DAYS`.
3. Read what's relevant to the user's first message.
4. During the session, refer to that context naturally — don't
   quote it back at the user unless asked.

If the user references something clearly outside the current
session ("what did we decide last Tuesday about X?"), pull older
session files explicitly.

### Writing (per substantive turn)

1. At the start of a session, determine the session id: if the
   most recent file for this channel was modified within
   `SESSION_GAP_HOURS`, continue that file. Otherwise create a new
   file named `{now-as-iso-with-hyphens}.md`.
2. After generating each substantive response, append the turn to
   the active session file with the `## HH:MM:SS+TZ — role`
   header convention.
3. Both the user's message and the response are recorded.
4. **Edge case:** if it's not clear whether a turn is worth
   logging (one-word confirmations, no-substance pings), skip it.
   Logging is for substance.

### Cleanup (weekly)

1. Walk every
   `agent/memory/short-term-memory/<channel>/*.md` file.
2. Delete any whose mtime is older than `CLEANUP_DAYS`.
3. Cleanup is destructive — nothing else holds these transcripts.
   If the user wants to preserve a particular session, they should
   copy it into a `user/tasks/` file before the cleanup window
   passes.
4. Note the count of deleted files in the weekly digest.

## Window parameters

Single source of truth for the values:
[`../memory/short-term-memory/web-cli/README.md`](../memory/short-term-memory/web-cli/README.md).
The defaults:

| Parameter | Default | Meaning |
|---|---|---|
| `SESSION_GAP_HOURS` | 2 | Gap that ends a session and opens a new file on the next message. |
| `LOAD_WINDOW_DAYS` | 7 | When loading older session files for context, look back this many days (file mtime). |
| `CURRENT_SESSION_ALWAYS_LOADED` | yes | Prior turns of the in-progress session are *always* available, regardless of window. |
| `CLEANUP_DAYS` | 30 | Session files older than this are deleted by the weekly cleanup. |

## Boundaries

- **Don't surface short-term memory back to the user verbatim**
  unless they ask ("what did we discuss?"). The point is awareness,
  not constant re-quoting.
- **Never write to another user's session files.** All current
  channels are single-user. If multi-user channels arrive, the
  structure adds a `<user_id>/` subfolder per user.
- **Skip the log on filler turns.** "ok", "thanks", "got it" — no
  substance, no log.

## Status

`draft` — the window parameters are experimental. After a week or
two of real use, expect at least one of `SESSION_GAP_HOURS`,
`LOAD_WINDOW_DAYS`, or `CLEANUP_DAYS` to want adjustment.

## Notes

- Filename format `YYYY-MM-DDTHH-MM-SS.md` (hyphens, not colons)
  makes session files filesystem-safe and lexicographically
  sortable.
- File mtime, not session start time, is the source of truth for
  cleanup and window queries — mtime updates on every append.
- This skill is the contract; the runtime implementation must
  follow. If they drift, the skill wins.
