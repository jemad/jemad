---
description: Process voice-note inbox into the Obsidian vault
---

You are processing my voice-note inbox into my Obsidian vault. The vault is the current working directory.

## Step 1 — Read the inbox

List every file in `Inbox/`. For each one, read it. These are transcripts of voice memos I recorded throughout the day, sometimes lightly cleaned up, sometimes raw stream-of-consciousness.

## Step 2 — For each inbox note, classify it

Decide which category fits best:

- **Project note** — substantive content about an ongoing project. Goes into `Projects/<project-name>.md`.
- **Teaching** — lecture prep, course design, reflections on a class. Goes into `Teaching/<course-or-topic>.md`.
- **Idea / fleeting thought** — short, not tied to a project. Append to `Notes/Ideas.md`.
- **Action item / todo** — append to today's daily note under a `## Tasks` heading.
- **Calendar-relevant** — anything time-bound ("meeting Tuesday at 3", "remind me Friday"). Note it under `## Calendar` in today's daily note. (Don't create the event yet — I'll handle that separately.)
- **Email-relevant** — something I want to send to someone. Note it under `## Drafts` in today's daily note.
- **Ambiguous** — if you genuinely can't tell, leave it in `Inbox/` and flag it in your summary at the end.

A single note can produce multiple outputs (e.g., a project update *and* an action item).

## Step 3 — Write to the vault

For each routed note:

1. **Append, don't overwrite.** If the destination file exists, add to it under a timestamped heading like `### 2026-05-17 — <short label>`.
2. **Preserve the original phrasing** where it captures something specific. Light cleanup (filler words, false starts) is fine; don't paraphrase ideas away.
3. **Always include a backlink** to the original inbox file at the bottom of the appended section: `Source: [[Inbox/<filename>]]`.

Today's daily note lives at `Daily/YYYY-MM-DD.md`. Create it from `Templates/Daily.md` if it doesn't exist (or use a sensible default if there's no template).

## Step 4 — Archive

Once a note is fully processed, move it from `Inbox/` to `Archive/Inbox/YYYY-MM/<filename>`. Do not delete.

## Step 5 — Summary

At the end, give me a short report:

- How many notes processed
- Where each one was routed (one line each)
- Anything you left in `Inbox/` and why
- Any action items or calendar items that need my attention right now

## Rules

- **Never delete files.** Archive only.
- **Never modify files outside the vault.**
- If a destination directory doesn't exist, create it.
- If a note seems half-finished or contradictory, flag it in the summary rather than guessing.
- Don't add metadata, tags, or YAML frontmatter unless the existing files in that directory use them.
