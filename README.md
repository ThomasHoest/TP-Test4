# Paul — your Chief of Staff

Welcome — this is your assistant's workspace.

This repository is the working memory you and your assistant share.
Conversations, notes, drafts, decisions, and the journal of how the
assistant is thinking alongside you all live here.

You own it. Lintel never reads from it. The in-tenant runtime that
handles your chat sessions is the only system that touches these
files.

## Two top-level folders

| Folder | Contains |
|---|---|
| [`user/`](user/) | Material *about* and *for* you — your profile, your network, your work, the digests the assistant produces. |
| [`agent/`](agent/) | The assistant itself — voice, boundaries, routines, memory, skills. |

## Where things live

- [`user/profile/`](user/profile/) — who you are: identity, situation, goals, working patterns.
- [`user/people/`](user/people/) — your network. One file per person.
- [`user/tasks/`](user/tasks/) — work in flight: drafts, briefs, applications.
- [`user/digests/`](user/digests/) — daily and weekly digests, committed for history.
- [`agent/persona.md`](agent/persona.md) — which voice your assistant is set to (The hard question).
- [`agent/boundaries.md`](agent/boundaries.md) — what the assistant can do for you and how autonomous you'd like it to be.
- [`agent/routines.md`](agent/routines.md) — recurring things the assistant can do on a schedule.
- [`agent/memory/`](agent/memory/) — the assistant's curated memory: decisions, observations, the running log.
- [`agent/skills/`](agent/skills/) — the atomic capabilities the assistant invokes.

## How to interact

The assistant lives at `thoughtpartner.online/cli` — sign in and chat.
Anything you'd want it to know about you goes in `user/profile/`. New
drafts and ongoing work goes in `user/tasks/`. The assistant reads
from this repo before every reply and writes back to it when there's
something worth keeping.

## Staff access

Lintel staff can read this repository, but only under one strict rule:
**every staff read commits a row to `agent/memory/staff-access.log`**
naming who read what, when, and for what reason. The log doesn't
exist in your repo yet — it's created on the first staff read, never
on provisioning, because most accounts never have one. If you ever
see that file, you can read its history in `git log` to know exactly
what happened.

## How to reset

Delete what you like. The assistant re-seeds missing structural files
on the next conversation, but it never recreates content you've
removed. If you want to start a section fresh, removing the file is
the right move; the structure repairs itself.
