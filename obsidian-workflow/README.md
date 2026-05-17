# Obsidian Capture-and-Process Workflow

A two-stage system for voice-noting thoughts on the go and routing them into an Obsidian vault at the desk.

## Architecture

```
Phone (any of the capture paths below)
    ↓
GitHub: <user>/obsidian-inbox     (or Dropbox folder — both can coexist)
    ↓
Desktop pulls / syncs
    ↓
Claude Code on desktop runs /process-inbox
    ↓
Local Obsidian vault on Dropbox — organized notes, daily notes, project files
```

## What lives where

| Thing | Where | In git? |
|---|---|---|
| Obsidian vault (everything organized) | `~/Documents/ObsidianVault` (Dropbox-synced) | **No** — stays as-is |
| Inbox repo (raw voice captures awaiting processing) | `~/git/obsidian-inbox`, mirrored to GitHub | **Yes** — dedicated repo |
| `/process-inbox` slash command | `~/.claude/commands/process-inbox.md` | n/a — local on desktop |

The vault is **not** in git. The inbox is. They're deliberately separate.

## Capture paths (pick one per moment; they coexist)

### A. Quick fire-and-forget — recommended for fleeting thoughts
- iOS/Android Shortcut: record audio → Whisper API transcribes → save .md to a Dropbox folder
- That Dropbox folder is either (a) the inbox repo's local clone (the desktop commits/pushes on a schedule), or (b) a folder inside the vault that `/process-inbox` reads directly
- Pro: 2 taps. Silent. Cheap (~$0.006/min of audio).
- Con: raw dump — no refinement before saving.

### B. Conversational capture via mobile Claude Code
- Open Claude Code on phone, scoped to the inbox GitHub repo
- Use `inbox-capture-prompt.md` (in this folder) as the session prompt
- Talk it through; the session commits and pushes
- Pro: think out loud, get a cleaner note, optional clarification questions.
- Con: cold-start overhead per note; costs tokens.

### C. Type directly in GitHub or a mobile git app (e.g. Working Copy)
- For thoughts you'd rather type than say
- Same destination, same result

All paths land in the same `Inbox/` (or repo root) location.

## Desktop processing

When you sit down at the desk:

1. Open Claude Code in any directory (the slash command knows its paths).
2. Type `/process-inbox`.
3. It does:
   - `git pull` the inbox repo
   - Read each unprocessed note
   - Classify (project / teaching / idea / todo / calendar / email)
   - Append to the right files in the vault, with a source link back to the inbox file
   - Move processed notes to `Archive/YYYY-MM/` in the inbox repo
   - Commit and push the archive

Look at the summary it gives you. Anything ambiguous gets left in the inbox.

## One-time setup checklist

- [ ] Create a private GitHub repo (e.g. `obsidian-inbox`)
- [ ] Clone it locally: `git clone <url> ~/git/obsidian-inbox`
- [ ] Copy `process-inbox.md` to `~/.claude/commands/process-inbox.md` on the desktop
- [ ] Edit the two paths at the top of `process-inbox.md` to match your real vault + inbox-repo paths
- [ ] (Optional) Build the iOS Shortcut: record → Whisper API → save to Dropbox/inbox
- [ ] (Optional) Save `inbox-capture-prompt.md` somewhere accessible from the phone — paste it into mobile Claude sessions when you want conversational capture
- [ ] Decide where Dropbox-captured notes land: directly in the inbox repo, or in a vault `Inbox/` folder

## Design decisions worth remembering

- **Vault stays out of git.** The inbox is the only thing in GitHub. Keeps the vault simple and unchanged.
- **Inbox is a separate repo, not a branch.** Cleaner; single purpose.
- **Branches not needed inside the inbox repo.** Sequential single-user notes → commit to `main` directly.
- **Dispatch is not part of this workflow.** It requires the desktop to be awake, which defeats async capture.
- **Cloud sessions only capture; the desktop is the only processor.** Routing and classification always happen against the local vault, where the existing notes are.
- **Two capture paths coexist** because different moments want different tools (fast-and-silent vs. think-out-loud).

## Files in this folder

- `README.md` — this file
- `process-inbox.md` — the desktop slash command (currently lives at repo root; can be moved here)
- `inbox-capture-prompt.md` — the prompt to give mobile Claude Code sessions
