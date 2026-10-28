# 07 · Patching an agent you don't own

The agent I run ships as a package on a NAS appliance. I can't wait for upstream to fix things, and I can't fork it either. So I patch it in place and keep the patches in a repo that survives upgrades.

Three of those patches taught me more about the software than reading it ever did.

## The trigger that never fires

The bill arrived before the diagnosis did. A single day of hourly long-session usage, and the number was an order of magnitude above normal.

The cause was not a leak. It was a threshold that could not be reached. Compression was configured to fire at 50% of the context window — with a one-million-token window, that is 500,000 tokens. The offending session held 29,263 messages and never exceeded 82,000 tokens, because chat messages are short and tool output is capped. It was never going to fire. The session grew forever and every request re-sent all of it.

**The fix:** trigger on message count as well as token share — 60 user turns, keeping the last 30 intact.

## The fix that carried the same bug

My first version counted `len(messages)`.

A session with 17 real user turns held 682 messages, because one turn can produce dozens of tool calls and results. That session hit the threshold and compressed three times, flattening real history into summaries while the user was still working.

Counting messages to measure a conversation is the same category of error as measuring context in the wrong unit: the number went up, so something must have happened.

**The corrected version** counts only `role == user` messages that carry no `tool_call_id` and are not summary headers. Real turns.

If you take one thing from this file: **a trigger threshold must be expressed in the unit the user experiences.** Everything else grows on its own.

## The status message that went nowhere

Compression worked, silently. Users could not tell whether their history had been summarized or dropped.

The status callback existed and was being called. On the HTTP transport it went nowhere: that adapter's `send()` is a no-op stub, and the code path that builds the agent never passed a status callback in the first place. The message was emitted into a function that discards it.

**The fix:** route the notice through the streaming delta channel that the client actually renders, guarded so it only fires on that transport.

The general lesson is not about this codebase. When output disappears, trace the channel, not the call site. A message can be sent and still have nowhere to go.

## The debounce that reset every request

After the notice worked, it fired every single request.

In-memory debounce state lived on the compressor object. On the HTTP transport, a new agent object is built per request — so the baseline was reset before every check, and every check decided the conversation was overdue.

**The fix:** persist the baseline to session metadata on compress, restore it before checking.

Any state that must outlive a request has to be stored outside the object that serves the request. That sounds obvious until the object is silently re-created.

## Skill output, capped

Same bill, second cause: a tool that returned an entire skill document — 61 KB on the largest one — straight into context, on every load, and then re-sent with every subsequent request.

**The fix:** head 40% / tail 60% with a 20 KB cap and an explicit truncation marker. The head gives you the trigger and the first steps; the tail usually holds the pitfalls, which is the part people actually need.

## What I took from all four

- Read the trigger, not the feature name. A setting named `threshold` tells you nothing about the unit it uses.
- A fix inherits the blind spots of whoever wrote it. Audit your own patch with the same suspicion you applied to the original.
- When output vanishes, follow the channel to its endpoint.
- Anything that must survive a request boundary has to be written down somewhere durable.
- Version the patch separately from the product. Upgrades revert your work without telling you, and the second time you apply a patch from memory it will be subtly different.

No upstream contribution here — these are local patches against a moving target, re-applied after every upgrade and verified by a script that checks the patched symbols exist in the running install.
