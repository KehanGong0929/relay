# relay — session handoff for AI coding agents

Keep your working context alive across `/clear` and session boundaries. Pick up exactly where you left off — in the same agent or a different one.

## Install

I loved Matt Pocock's [`/handoff`](https://github.com/mattpocock/skills) skill but kept wanting more — a zero-input `/resume` that just continues, and a `/pickup` that lets me browse past sessions. So I built on top of it.

```
npx skills add github.com/KehanGong0929/relay -y -g
```

`-y` = non-interactive, `-g` = global (available in every project). Drop `-g` to install for the current project only.

## Commands

| Command | When | What it does |
|---------|------|--------------|
| `/handoff [purpose]` | End of session | Writes a handoff document to your OS temp dir. `purpose` is optional — if omitted, the agent infers it from the conversation. |
| `/resume` | Start of next session | Auto-loads the latest handoff for the current project and continues. No input needed. |
| `/pickup [keyword \| date \| path]` | Start of next session | No argument: shows the 10 most recent handoffs to choose from. With an argument: filters by keyword, date (`2026-06-07`), or file path. |

## The flow

```
# Session A — finish your work, then hand off
/handoff finish the auth middleware

# Manually start a fresh session (Claude Code built-in, not part of relay)
/clear            # or open a new window in the same folder

# Session B — continue exactly where you left off
/resume
# …or pick a specific one
/pickup 2026-06-07
```

## Designed for Claude Code, works across agents

`relay` was built for **Claude Code** but handoff documents are plain markdown — no dependency on any specific agent's internals.

A handoff written in Claude Code can be resumed in **Codex**, **Copilot CLI**, or any agent that can read files. Each skill is a plain-instruction `SKILL.md` that uses the host agent's own file tools — no code, no runtime, nothing to install besides the skills themselves.

```
Claude Code  ──/handoff──▶  handoff.md  ──/resume──▶   Claude Code (new session)
                                         ──/pickup──▶   Codex
                                         ──/resume──▶   Copilot CLI
                                         ──/pickup──▶   any other agent
```

## How resume and pickup find your project

Both skills glob `handoff*.md` in your OS temp dir and identify the right project by checking whether a document references your **current working directory path** — not by filename. This means:

- Works even if the file was renamed or written by a different agent
- `/resume` picks the newest match for the current project automatically
- `/pickup` lets you browse, filter by keyword, date, or path, and choose

## Credits / license

The `/handoff` skill is derived from [mattpocock/skills](https://github.com/mattpocock/skills) (MIT). `/resume` and `/pickup` are original to this pack. See `LICENSE`.
