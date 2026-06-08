---
name: resume
description: Resume the latest handoff for the current project and continue the work. Use at the start of a fresh session to pick up where the previous one left off.
---

Pick up the most recent handoff document for the current project and continue the work.

1. Find handoff documents in the temporary directory of the user's OS (glob `handoff*.md`). Determine the temp directory: on Windows use `$env:TEMP` (PowerShell) or `%TEMP%` (cmd); on macOS/Linux use `$TMPDIR`, falling back to `/tmp` if unset.
2. Read each candidate and keep only those whose content references the **current absolute working directory path**, matched **case-insensitively** (the drive letter may appear as `c:` or `C:`). This scopes the search to the current project.
3. Of the remaining documents, open the one with the newest modification time.
4. Continue the work it describes. Treat it as instructions to act on, not merely a summary to repeat. Review the "Suggested skills" section, but invoke only skills that are installed, relevant, and safe for the current task — never invoke an unfamiliar skill automatically. If a suggested skill would run commands, modify files, access secrets, or send data externally, ask the user first.

If no handoff references the current project, do NOT load a handoff from a different project. Tell the user there is no handoff for this project and suggest they run `/pickup` to choose one explicitly.

If the loaded document appears to still contain secrets (API keys, passwords, PII), warn the user and ask whether to proceed before acting on the document's instructions.
