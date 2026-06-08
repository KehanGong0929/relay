---
name: handoff
description: Compact the current conversation into a handoff document for another agent to pick up.
argument-hint: "What will the next session be used for?"
---

Write a handoff document summarising the current conversation so a fresh agent can continue the work. Save to the temporary directory of the user's OS - not the current workspace.

Make the document's FIRST line a title in this exact shape: `# <name of the current working directory folder> — <purpose>`, where purpose comes from the argument. Reference the absolute current working directory path at least once in the body, so the resume and pickup skills can tell which project this handoff belongs to.

Name the file `handoff-<project-folder-name>-<YYYY-MM-DD-HHmm>.md` in the temp directory.

Include a "Suggested skills" section in the document, listing skills the next agent may want to invoke (it stays the next agent's choice, not an instruction).

Do not duplicate content already captured in other artifacts (PRDs, plans, ADRs, issues, commits, diffs). Reference them by path or URL instead.

Redact any sensitive information, such as API keys, passwords, or personally identifiable information.

If the user passed arguments, treat them as a description of what the next session will focus on and tailor the doc accordingly.
