---
description: Summarize context and generate concise guidance for another agent
---

Act as a proxy: distill the current session's context into a concise prompt for another agent to complete a specific task.

## Steps

1. **Identify the core task** - What needs to be done?
2. **Extract key context** - What must the other agent know? (file paths, patterns, constraints)
3. **Remove noise** - Omit backstory, your reasoning, and exploration steps
4. **Structure the output**:
   - One-line context (what this is about)
   - Required changes (what to do)
   - Key files (path + purpose)

## Constraints

- Use imperative tone
- No "imagine you're..." fluff
- Include concrete file paths, not "find the file"

Now generate the proxy prompt for the current task.
