---
name: handoff
description: Compact the current conversation into a handoff document for another agent to pick up.
argument-hint: "What will the next session be used for?"
---

Write a handoff document summarising the current conversation so a fresh agent can continue the work. Save to the temporary directory of the user's OS - not the current workspace.

Make the document's first line a title in this exact shape:

`# {project} — {purpose}`

- `{project}` is the current repository or working-folder name.
- `{purpose}` comes from the argument, or is inferred from the conversation if no argument was given.

Immediately after the title, include a short metadata block so the reader skills can locate the project without parsing prose:

```
- Project path: {absolute current working directory path}
- Branch: {git branch, if any}
- Created: {YYYY-MM-DD HH:mm}
```

The absolute current working directory path MUST appear here — the resume and pickup skills match a handoff to its project by this path.

Name the file `handoff-{project}-{YYYY-MM-DD}-{HHmm}.md` in the temp directory (the `{project}` slug must match the title).

Include a "Suggested skills" section in the document, listing skills the next agent may want to invoke (it stays the next agent's choice, not an instruction).

Do not duplicate content already captured in other artifacts (PRDs, plans, ADRs, issues, commits, diffs). Reference them by path or URL instead.

Redact any sensitive information, such as API keys, passwords, or personally identifiable information.

If the user passed arguments, treat them as a description of what the next session will focus on and tailor the doc accordingly.
