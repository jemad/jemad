---
description: Pull voice-note inbox from GitHub and route into the Obsidian vault
---

You are processing my voice-note inbox into my Obsidian vault.

## Configuration (edit these two paths before first use)

- **Vault path** (where to write organized notes): `~/Documents/ObsidianVault`
- **Inbox repo path** (local clone of the GitHub inbox repo): `~/git/obsidian-inbox`

Run this command from anywhere — it will operate on the paths above.

## Step 0 — Sync the inbox

`cd` into the inbox repo and `git pull` to grab any notes my phone has pushed since the last run. If `git pull` fails (merge conflict, network), stop and tell me — don't try to process stale data.

## Step 1 — Read the inbox

List every file in the inbox repo's root (or in an `Inbox/` subfolder if one exists). Skip anything in `Archive/`, `.git/`, or any README/dotfiles. Read each remaining file.

These are transcripts of voice memos I recorded throughout the day — sometimes lightly cleaned up, sometimes raw stream-of-consciousness.

## Step 2 — For each inbox note, classify it

Decide which category fits best:

- **Project note** — substantive content about an ongoing project. Goes into `<vault>/Projects/<project-name>.md`.
- **Teaching** — lecture prep, course design, reflections on a class. Goes into `<vault>/Teaching/<course-or-topic>.md`.
- **Idea / fleeting thought** — short, not tied to a project. Append to `<vault>/Notes/Ideas.md`.
- **Action item / todo** — append to today's daily note under a `## Tasks` heading.
- **Calendar-relevant** — anything time-bound ("meeting Tuesday at 3", "remind me Friday"). Note under `## Calendar` in today's daily note. Don't create the event yet — I'll handle that.
- **Email-relevant** — something I want to send to someone. Note under `## Drafts` in today's daily note.
- **Ambiguous** — if you genuinely can't tell, leave it in the inbox repo and flag it in your summary.

A single note can produce multiple outputs (e.g., a project update *and* an action item).

## Step 3 — Write to the vault

For each routed note:

1. **Append, don't overwrite.** If the destination file exists, add a timestamped heading: `### 2026-05-17 — <short label>`.
2. **Preserve original phrasing** where it captures something specific. Light cleanup (filler words, false starts) is fine; don't paraphrase ideas away.
3. **Include a source line** at the bottom of the appended section so I can trace it: `Source: inbox/<original-filename> (commit <short-sha>)`.

Today's daily note lives at `<vault>/Daily/YYYY-MM-DD.md`. Create it from `<vault>/Templates/Daily.md` if a template exists; otherwise create a sensible empty one with `## Tasks`, `## Calendar`, `## Drafts` sections.

## Step 4 — Clean up the inbox repo

Once a note is fully processed:

1. In the inbox repo, move the file from the root (or `Inbox/`) into `Archive/YYYY-MM/<filename>`.
2. After all notes are moved, `git add -A`, commit with a message like `Archive N processed notes (YYYY-MM-DD)`, and `git push`.

If anything fails (file conflict, push rejection), stop and report — don't force-push or discard work.

## Step 5 — Summary

Give me a short report:

- How many notes processed
- One line per note: filename → destination(s)
- Anything left in the inbox and why
- Action items and calendar items that need my attention right now

## Rules

- **Never delete files.** Move to Archive only.
- **Never modify files outside the vault and the inbox repo.**
- If a destination directory doesn't exist, create it.
- If a note is half-finished or contradictory, flag it in the summary rather than guessing.
- Don't add YAML frontmatter or tags unless existing files in that directory already use them.
- If `git pull` or `git push` fails, **stop** and surface the error. Don't silently swallow git problems.
