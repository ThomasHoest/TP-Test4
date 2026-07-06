# User — material about and for you

Everything *about* and *for* you. The assistant
itself lives under [`../agent/`](../agent/).

## Folders

- [`profile/`](profile/) — identity, situation, goals, working
  patterns. The assistant reads from here at the start of every
  session.
- [`people/`](people/) — your network. One file per person, with
  context, last touch, suggested follow-up.
- [`tasks/`](tasks/) — ongoing work: drafts, briefs, applications,
  speeches. Naming keyed to the *relevant* date, not creation date.
- [`digests/`](digests/) — generated daily and weekly digests.
  Committed for history and pattern review.

This split mirrors the assistant's mental model: who you are
(`profile/`), who's in your orbit (`people/`), what you're working
on (`tasks/`), and what the assistant produced for you (`digests/`).
