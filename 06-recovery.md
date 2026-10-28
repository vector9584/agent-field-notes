# 06 · Surviving compaction

## The problem

Long conversations get compressed. Compression is lossy, and it is lossy in a specific direction: it keeps the narrative and drops the operational detail — which file, which number, which rule.

The agent then continues confidently from a summary that is 90% right. The 10% it lost is usually the part that mattered.

## What actually broke

A question arrived mid-task: *"how's it going"*.

That question contains no domain keywords. The agent's skill index is matched by keyword, so no skill loaded. The rule that governed the task — a counting rule, written at the top of a skill — was never in context.

The result: two events were silently dropped from a total. Eleven became nine. Everything downstream was consistent with nine.

The failure was not the compaction. The failure was that a critical rule lived somewhere that only loaded for certain phrasings of the question.

## Three fixes that worked

**Put rules about the conversation in the rule layer, not in a skill.** A skill loads when the topic matches. "How's it going" matches nothing. Rules that must always apply belong where they are always present, or they are decoration.

**Answer status questions from state, not from memory.** The agent keeps a task list. When asked for progress, it reads the list first and answers three things: what is done (with evidence), what is running (and for how long), what is blocked (and on whom). Never re-explore, never restart finished work.

**Re-load what was pruned.** Compression marks stale content as removed, and the marker is easy to miss while the model keeps talking as if it remembers. When a procedure is about to be used, check that its body is actually present. Reloading costs one call; getting it wrong costs the task.

## The habit that prevents most of this

End each working session by writing down what would be expensive to rediscover: the paths, the decisions, the reasons. Three hundred words.

The next session starts from that note instead of from a summary of a summary. Compaction becomes survivable because the important things were already copied somewhere that compaction does not touch.
