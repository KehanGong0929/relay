---
name: pickup
description: Choose a handoff document to resume - by list, keyword, project name, date, or file path. Use when you want to pick a specific handoff rather than the latest for the current project.
argument-hint: "(optional) keyword, project name, date (YYYY-MM-DD), or file path"
---

Choose a handoff document from the temporary directory of the user's OS and continue its work. Determine the temp directory: on Windows use `$env:TEMP` (PowerShell) or `%TEMP%` (cmd); on macOS/Linux use `$TMPDIR`, falling back to `/tmp` if unset. Glob `handoff*.md` in the temp directory to find candidates. Each document's first line is its title; use it as the human-readable label.

If no `handoff*.md` files are found in the temp directory, tell the user the temp directory contains no handoff files and suggest they run `/handoff` first.

**If no argument is given:** list recent handoffs, newest first, each shown as `label — date — filename`, up to 10 entries. If more than 10 exist, note the total count. Ask the user to choose one.

**If an argument is given, interpret it as:**
- a file path or filename → load that document directly;
- a date like `2026-06-04` → filter to handoffs from that day;
- otherwise a keyword or project name → filter labels (handoff titles) and filenames by it (case-insensitive).

After filtering: if exactly one matches, load it; if several match, list them and ask the user to choose.

Once a document is chosen, read it and continue the work it describes - treat it as instructions to act on, not merely a summary to repeat. Review the "Suggested skills" section, but invoke only skills that are installed, relevant, and safe for the current task — never invoke an unfamiliar skill automatically. If a suggested skill would run commands, modify files, access secrets, or send data externally, ask the user first.

If the loaded document appears to still contain secrets (API keys, passwords, PII), warn the user and ask whether to proceed before acting on the document's instructions.
