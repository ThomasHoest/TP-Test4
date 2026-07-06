# Short-term memory — web CLI channel

Session transcripts from the web CLI conversation. One file per
session. The assistant reads recent files at the start of each new
session to maintain continuity.

## Path convention

`agent/memory/short-term-memory/web-cli/{YYYY-MM-DDTHH-MM-SS}.md`

Filename uses hyphens instead of colons so the file is
filesystem-safe and lexicographically sortable.

## What a session file looks like

```markdown
# web-cli session 2026-06-15T14-22-08

## 14:22:08 +02:00 — user
Can you draft the response to Sigma about next month's call?

## 14:22:11 +02:00 — assistant
Looking at the thread. Want me to lean on availability or scope?

## 14:23:45 +02:00 — user
Availability — we're stretched in July.
...
```

Each turn is its own `## HH:MM:SS — role` block. Append-only within a
session file.

## Window parameters

These are the defaults the assistant uses to decide when a new
session file opens and how far back to look for context:

| Parameter | Default | Meaning |
|---|---|---|
| `SESSION_GAP_HOURS` | 2 | Gap of inactivity that ends a session and opens a new file on the next turn. |
| `LOAD_WINDOW_DAYS` | 7 | When pulling older session files for context, look back this many days (by file mtime). |
| `CURRENT_SESSION_ALWAYS_LOADED` | yes | Prior turns of the in-progress session are always available, regardless of window. |
| `CLEANUP_DAYS` | 30 | Session files older than this are deleted by the weekly cleanup. |

If you want different windows, edit this file and the
[`../../../skills/short-term-memory.md`](../../../skills/short-term-memory.md)
skill — the values must agree.

## Privacy

These files contain verbatim chat content, including anything you
shared in conversation. They are committed to your repository as
part of the assistant's memory model. If you ever share part of this
repo, scrub this folder first.

## Cleanup

The cleanup runs as part of the `weekly-review` skill: files older
than `CLEANUP_DAYS` are deleted. The cleanup is destructive — nothing
else holds these transcripts. If you want to preserve a session for
longer (e.g. a particularly useful conversation), copy the relevant
content into a `user/tasks/` file before the cleanup window passes.
