# 03 · Where each thing belongs

## The rule

Four stores, one direction:

```
session  →  note  →  skill  →  index
(history)   (depth)   (procedure)  (pointer)
```

Put a thing in the wrong store and it is gone, even though it was written down.

## Why the wrong store is fatal

A procedure stored in a knowledge note is invisible at the moment you need it. The agent does not read notes before acting; it reads notes when asked a question. So the note sits there being true and useless.

A fact stored in a skill is worse. Skills load as instructions. A three-month-old price list inside a procedure will be followed confidently long after it stopped being accurate.

A durable fact stored only in conversation is the worst of the three. It survives until the window closes and then it never happened.

## The four stores, concretely

**Session history** — what was said and when. Searchable, never curated, grows without bound. Use it to answer "what did we decide about X", not "how do I do X".

**Knowledge notes** — the depth: why a system behaves the way it does, benchmark tables, architecture maps. Loaded when the question is analytical. Written for a reader who has time.

**Skills** — the procedure: trigger, numbered steps, exact commands, pitfalls. Loaded when the question is operational. Written for an agent in a hurry.

**Index** — one line per skill, always in context. Its entire job is to help the agent decide which body to load. It is not a summary and it must not grow into one.

## The inbox loop

A note-taking shortcut I added after the fourth time an instruction got lost:

Capture first, classify later. When I say "remember this", it goes into a single inbox file with a timestamp, verbatim — no attempt to decide where it belongs while the context is still fresh.

Then, at the end of each session, the agent walks the inbox and files each entry: a preference becomes a rule, a procedure becomes a skill, a fact becomes a note. Filed entries get deleted from the inbox.

Without the deletion step the inbox becomes a second history and stops being read. An inbox that is never emptied is a to-do list nobody trusts.
