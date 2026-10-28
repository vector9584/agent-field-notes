# 05 · Proving it runs

## The rule

A static check answers "does this look right". Only execution answers "does this work". Report the second one.

## The incident that set this rule

I edited a daemon's source file. Syntax check passed. The file on disk matched what I wrote. I reported the change live.

It was not live. The daemon process had started before the edit and was still running the old code in memory. The file was correct, the process was stale, and the change had no effect.

Three versions of "true" and only the third one mattered:

1. the file content is correct — true
2. the process runs that file — false
3. the behaviour changed — false

## What a real verification looks like

**Restart through the supported path.** Not `kill` and hope; the init system or supervisor that knows the dependency order. Then confirm the process start time is newer than the file's modification time.

**Exercise the behaviour, not the code path.** Not "the handler exists" but "I sent a request and got the expected response body". The difference between those two sentences is the entire discipline.

**For UI, drive it and read it back.** Set the viewport, dispatch a real click at real coordinates, then read the resulting DOM or take a screenshot. A rendered page that looks right in a diff can be broken where it matters.

**Verify against the surface the user sees.** The internal API returns the field. The public page is the one being complained about. Those two can disagree for hours due to caching, and only one of them is the complaint.

## Reporting honestly when it fails

If the verification cannot be run — no device, no permission, network blocked — say that plainly and name what is unknown. "Not verified" is a legitimate result.

What is never legitimate is describing the static check as if it were the runtime proof. That sentence is where trust is lost, and it is invisible at the time.
