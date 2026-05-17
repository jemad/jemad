# Git, Obsidian, and the Claude family — reference notes

Background context discussed earlier in the design conversation. Lives alongside the workflow README so the design decisions are traceable.

## The Obsidian Git plugin

An Obsidian community plugin (`Obsidian Git`) that turns your vault into a git repo with auto-commit/auto-push on a configurable interval (e.g., every 10 minutes). Bidirectional: it pulls on Obsidian startup too.

What it gives you if you enable it:
1. **Version history of the vault.** Every change is a commit. `git log` to see what a note looked like last Tuesday. Much cleaner than Dropbox's built-in version history (which is time-limited and per-file).
2. **Backup independent of Dropbox.** A second cloud copy. Defends against accidental delete-and-sync.
3. **Cloud processing of the vault itself.** A cloud Claude session (Claude Code on web/mobile) can clone the repo and operate on your *existing* notes — not just incoming captures.
4. **Multi-device editing without sync conflicts.** Less of a concern if you only edit on one machine.

## Why we decided NOT to put the vault in git (for now)

The chosen architecture splits things on purpose:

- **Inbox** → in git (a dedicated repo, e.g. `obsidian-inbox`). Phone captures push here.
- **Vault** → NOT in git. Stays on Dropbox, exactly as it is today. Desktop reads from inbox repo and writes into the vault.

This was the cleanest fit because none of the four reasons above were active needs:
- Dropbox versioning is acceptable for now
- Dropbox already provides backup
- We're not asking cloud Claude to *process the existing vault* — only to *deposit captures*
- Single-device editing

**Trigger to revisit:** the day you want a cloud Claude to do something like *"summarize everything I've written about Project X this month"* without touching the desktop, you'd want the vault in git too.

## Claude Desktop vs. Claude Code — file-access summary

| Claude product | Can edit local files? | Can git-clone/push? | Best for |
|---|---|---|---|
| Claude chat (claude.ai, mobile, desktop app) | Via connectors only (Drive, Box, etc.); no native vault access | Indirectly via GitHub connector if enabled | Conversation, lookup, generating text |
| **Claude Desktop** (the desktop app with MCP servers) | **Yes** — direct filesystem MCP can read/write your local vault | Yes via terminal MCP or shell access | Chat-style interaction with your local vault |
| **Claude Code (local CLI)** on the desktop | **Yes** — runs as a process in a directory, full read/write | Yes, natively (it's a CLI in a real shell) | Multi-step work in a vault: routing notes, batch edits |
| **Claude Code on web/mobile** (cloud sessions) | Only files inside its ephemeral container — **cannot reach your laptop** | Yes, against repos it's been given access to | Operating on cloud-hosted repos/data without your machine being on |

For the chosen workflow:
- **Mobile cloud Claude Code** = the *capture* endpoint (writes to inbox repo on GitHub)
- **Local Claude Code on the desktop** = the *processor* (reads inbox repo, writes vault)

## Dispatch — why it isn't part of this workflow

Dispatch sends a task from your phone to your paired desktop, which has to be awake and running the Claude app. Each dispatched task spins up a **new, isolated session** with no access to your existing Cowork Projects, working directory, or memory (current limitation; tracked in upstream issues).

For voice-note capture that's supposed to work *whether or not the desktop is on*, Dispatch is the wrong shape. The inbox-repo approach is async by design: phone pushes whenever, desktop pulls whenever.

Dispatch is still useful for other things (one-off tasks you want a desktop to handle while you're on the go) — just not for this capture pipeline.

## What lives in this repo (the inbox repo) for a mobile session to read

When a mobile Claude Code session is scoped to the inbox repo, these files are right there in its working directory — it can `cat` them as part of its context:

- `README.md` — the workflow architecture, so the session understands its role
- `inbox-capture-prompt.md` — the actual prompt to follow when saving a note
- `git-and-obsidian.md` (this file) — design rationale, in case the session needs to reason about why things are set up this way

This is the "free context" benefit you noticed: the documentation lives **with** the data, so any new session is self-orienting.

## Decision matrix: should I put my vault in git later?

| Signal | Action |
|---|---|
| You want to ask cloud Claude questions about your existing vault | → put vault in git |
| You're editing the vault from a second device and getting sync conflicts | → put vault in git |
| You want richer version history than Dropbox provides | → put vault in git |
| You're happy with current Dropbox behavior and process at the desk | → leave vault alone |

If/when you decide to do it: install Obsidian Git, point it at a new private repo (`obsidian-vault` or similar — *separate* from the inbox repo), set auto-commit to ~10 min. The inbox-and-process workflow doesn't need to change.
