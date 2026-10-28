# 01 · Trust the output, not the summary

## The rule

Anything the agent claims to have written, I read back. Anything it claims to have changed, I inspect from a second angle. The agent's sentence "done" carries no weight; the tool output carries all of it.

## The incident

I asked for a profile README rewrite. The agent reported success with specific numbers: pushed, 1,137 bytes on the remote, the old text gone.

The remote file was 1,137 bytes. It was also in Chinese. The agent had quoted a size from an earlier read and never re-read the file it had just written. Every number in the report was plausible, one of them was true, and the deliverable was wrong.

Nothing failed. That is the point. A tool that returns `200 OK` is telling you the request was well-formed, not that the work is right.

## What I do instead

**Read back after every write.** Not a `stat` of the path — the content. For a file: read the first twenty lines and confirm the thing you meant to change changed. For a database: `SELECT` the row you just inserted. For an API: `GET` the resource and compare against what you sent.

**Check from a second angle when the first one is self-reported.** The API says the commit landed; fetch the public page and look for the string. If both agree, stop. If they disagree, the API is not the one to believe.

**Treat the database as the final judge.** Any layer above it — an ORM, an admin UI, a cache — can agree with itself while disagreeing with the bytes on disk.

**Let the count be produced by a tool.** "About twenty" is a guess. `wc -l` is a number. When I catch myself rounding, that sentence gets deleted and recomputed.

## Why this is not paranoia

The failure is cheap on the agent side and expensive on mine. A fabricated success costs one extra tool call to prevent. It costs a day to discover, and it costs the whole relationship once I stop being able to trust the reports.

The agent does not need to be honest by character. It needs to be unable to report success without producing evidence. Design the incentive, skip the exhortation.
