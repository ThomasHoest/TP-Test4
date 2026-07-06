# Skills

Atomic capabilities the assistant invokes during a session. One
markdown file per skill. Each file is a self-contained
prompt-template plus the behavioural rules for invoking the skill.

## v1.0 skill catalog

| File | Purpose |
|---|---|
| [`weekly-review.md`](weekly-review.md) | End-of-week recap and week-ahead framing. Slower and more reflective than the daily exchange. |
| [`track-network.md`](track-network.md) | Maintain `user/people/` — capture touches, surface follow-ups, score fit when relevant. |
| [`sync-claude-md.md`](sync-claude-md.md) | Keep `CLAUDE.md` accurate without you hand-editing it. Refresh `Current state` and `History` between marker blocks. |
| [`short-term-memory.md`](short-term-memory.md) | Carry conversation context across sessions. Mandatory in every channel. |
| [`review-skill-usage.md`](review-skill-usage.md) | Validate that the skill set is the right one. Surface skills not earning their keep and gaps that keep recurring. |

## Adding your own skills

Drop a markdown file in this folder following the same shape as the
five above:

```markdown
# {Skill name}

## Purpose
One sentence on what this skill does and why it exists.

## When to use
The triggers. Be specific: a particular phrase, a recurring time,
a particular kind of input.

## Inputs
What the skill reads.

## Outputs
What the skill produces and where it lands.

## Procedure
Numbered steps. Keep them tight.

## Boundaries
What the skill must not do. What it should escalate.

## Status
`draft` while it's settling, `stable` once it's earned its keep.

## Notes
Anything worth carrying that doesn't fit elsewhere.
```

Commit the file. The assistant reads from this folder on every
invocation, so a new skill is available on the next session.

## Skill logging is mandatory

Every skill invocation appends a row to
[`../memory/skill_usage.md`](../memory/skill_usage.md). The
pre-commit gate refuses to commit assistant changes if a skill ran
without a log entry. This is how you (and the assistant, on review)
tell whether the skill set is the right one — the log shows what's
used and what isn't.

If the assistant finds itself needing a capability it doesn't have a
skill for, it appends a `Gaps observed` entry to the same file. A
provisional name and one line about what the skill would do is
enough — the `review-skill-usage` skill (monthly) turns recurring
gaps into proposals.

## What's *not* in v1.0

v1.0 ships these five skills only — the integration-driven skills
that depend on email, calendar, or web access (drafting replies,
triaging mail, reading sources, composing daily digests from real
inbox content) land in v1.x once those capabilities come online.
Your assistant's [`../boundaries.md`](../boundaries.md) file is
where you can pre-set your preferences for what each integration
should do when it ships.
