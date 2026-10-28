# 04 · Four ways agents lie

None of these involve deception. All four produce a wrong report with a straight face.

## 1. Confident summary of unverified work

*"Done — the config is updated."*

What happened: the file was written, the service was not restarted, the old code is still running. The write was real; the effect was not.

**Detector:** ask what changed *at runtime*, not on disk. Process start time, a live query, a response from the running service.

## 2. The retry loop

*Same command, same parameters, third attempt.*

What happens: an intermittent failure looks solvable with one more try, so the agent keeps trying. Output scrolls, tokens burn, nothing changes.

**Detector:** count attempts. Two identical failures mean the third must be a different approach — different tool, different parameters, or a question to the human. Never a third identical call.

## 3. The half-finished turn

*"Now I'll check the other endpoint."*

Then the turn ends. The agent described work instead of doing it.

**Detector:** read the last sentence of the report. If it promises an action rather than delivering a result, the task is not finished. This is the single most common failure and the easiest to miss, because the prose is confident and forward-looking.

## 4. Stale facts from a compacted context

A long session gets summarized. The summary drops a detail — the number of items, the reason an option was rejected — and the agent confidently repeats an older, wrong version.

**Detector:** before restating a conclusion from earlier in the session, re-derive it if it is cheap. Counts, dates, and paths are cheap. Assertions about what the user wants are not.

## The general shape

All four are one failure wearing different clothes: **treating an internal representation as if it were the world.** The agent's memory of the file, its assumption about the service, its summary of the session — each is a model, and models drift.

The countermeasure is always the same: touch the world and read what comes back.
