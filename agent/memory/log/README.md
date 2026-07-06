# Log — chronological scratch

Daily entries the assistant writes at the end of a working session.
Captures what ran, what surfaced, what you reacted to.

## Path convention

`agent/memory/log/{YYYY}/{MM}/{YYYY-MM-DD}.md`

One file per day. The file is created the first time the assistant
has something to log that day.

## What goes in a daily log entry

```markdown
# {YYYY-MM-DD}

## What ran
- Skills invoked, with one-line summaries.

## What surfaced
- New material the assistant noticed: an opportunity moved, a
  person changed roles, a topic shifted.

## What you reacted to
- What you accepted, deferred, declined, or asked for a draft of.

## Notes
- Anything worth carrying forward that doesn't belong in a
  structured memory file yet.

## People
- Material changes to people files (role change, priority shift,
  new entry).
```

## What does NOT go in the log

- Raw chat transcripts → those live in
  `agent/memory/short-term-memory/<channel>/`.
- Persistent facts → those get promoted to `decisions.md`,
  `observations.md`, etc.
- Drafts → those go in `user/tasks/`.

The log is the working scratch. Things that earn their keep get
promoted; the rest sits here as a record that the assistant ran.

## Hygiene

Daily logs older than 60 days roll up into a monthly summary entry
at `agent/memory/log/{YYYY}/{MM}/monthly-summary.md`, then the
dailies can be archived (moved out of `log/` into an archive folder
or deleted, depending on your preference). The canonical record of
decisions stays in `decisions.md` — the log is for chronology and
texture, not for things you need to find later by topic.
