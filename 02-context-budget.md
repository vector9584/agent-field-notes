# 02 · Context is a budget, not a bucket

## The observation

Cost does not scale with what the agent reads. It scales with what it re-reads. A long session on a cheap model can cost more than a short one on an expensive model, because every turn re-sends the history and pays cache-read rates on all of it.

The expensive number is not the prompt you wrote. It is the conversation you never closed.

## What the numbers looked like

Skills: 274 documents, 2.8 MB of text. Loading them naively is impossible — and unnecessary, because the agent only needs the titles to decide what to load.

That distinction is the whole trick:

- **Index** — one line per skill, always present, a few thousand characters.
- **Body** — the actual procedure, loaded on demand, sometimes 40,000 characters.

Mixing them is what makes an agent expensive and slow. An index that inlines its archive is a 2.8 MB prompt.

## The three moves

**Cap what enters, in the shape it enters.** Large skill bodies get split into a main file plus references; a 40,000-character procedure becomes 6,000 up front and four files behind it. A 200 KB tool output gets truncated to the part that changes a decision.

**Compress the conversation before it compresses you.** Long sessions get summarized on a schedule rather than after the model starts dropping the middle. The summary keeps decisions and paths; it discards the exploration that led there.

**Close sessions that are done.** A finished task that stays open keeps paying rent. Export it, distill what mattered into a note or a skill, start clean.

## What to spend it on

There is a real trade-off here and it is not "spend less". Spend on the things that are expensive to reconstruct:

- the exact path of a file that took six attempts to find
- the reason an approach was abandoned
- the shape of a data structure that is not documented anywhere

Do not spend on: the full text of a document the agent can re-fetch, the reasoning that led to an obvious conclusion, or a restatement of the question.
