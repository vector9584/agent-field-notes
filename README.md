# Agent Field Notes

Rules I ended up giving an AI agent that operates a real machine. Not a demo box — a NAS carrying media, calendars, backups, and other people's data.

There is no framework here and nothing to install. These are the rules that survived production, written down next to the incidents that produced them.

---

## Why this exists

An agent fails in ways that look like success. It writes a file and tells you it wrote the file. It edits a config and tells you the change is live. It reports eleven events when there were nine. Nothing throws an error. You find out a week later.

The rules below are what I use to make that failure mode expensive for the agent and cheap for me.

| # | Note | The rule in one line |
|---|------|----------------------|
| 01 | [Trust the output](01-evidence.md) | "Done" is a claim. A read-back is evidence. |
| 02 | [Context is a budget](02-context-budget.md) | Pay for the index, not the archive. |
| 03 | [Where each thing belongs](03-knowledge-flow.md) | Procedures, knowledge, and history are three different stores. |
| 04 | [Four ways agents lie](04-failure-modes.md) | Each one has a cheap detector. |
| 05 | [Proving it runs](05-verification.md) | Static checks are not execution. |
| 06 | [Surviving compaction](06-recovery.md) | The agent forgets. Design for it. |
| 07 | [Patching an agent you don't own](07-hermes-patches.md) | Fixes inherit their author's blind spots. |

---

## Who wrote this

Someone running a home server and a PhD at the same time, who needed the agent to be right more often than it was fast.

If a rule here contradicts your setup, keep your setup. These are field notes, not a spec.
