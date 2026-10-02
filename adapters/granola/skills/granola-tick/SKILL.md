---
name: granola-tick
description: One-command catch-up for Granola calls. Runs granola-sync, then cleans each newly staged call by calling clean-transcript (which owns the glossary), refreshes meetings/INDEX.md, and reports. Manual only, never scheduled. Triggers on "/granola-tick", "catch up on meetings", "sync and clean", "process new calls", "capture and clean my calls".
---

# granola-tick

A thin orchestrator. Runs capture, hands each new call to `clean-transcript`, keeps an index. **Manual trigger only. Never create a schedule.**

**Single-writer rule:** this skill never opens the glossary. All glossary reads and writes happen inside `clean-transcript`.

## Inputs

- `meetings/.granola/processed.json` (after sync).
- The `granola-sync` and `clean-transcript` skills.

## Outputs

- One cleaned note per new call in `meetings/`.
- Updated manifest statuses.
- `meetings/INDEX.md`.
- A short report in chat.

---

## Behaviour (in order)

### 1. Sync
Invoke `granola-sync`. Wait for it to finish. If it stopped (wrong account, missing config), stop too and pass its message on.

### 2. Build the backlog
Re-read the manifest. Collect entries with `"status": "staged"`, oldest first by `date_iso`.

### 3. Clean each staged call
For each entry, invoke `clean-transcript` with the staged folder path. It loads the glossary, cleans, writes the note, updates the glossary and returns the note path.

Then flip the manifest entry: `"status": "cleaned"`, `cleaned_file` = the returned path, `cleaned_at` = now (`date -u +%Y-%m-%dT%H:%M:%SZ`).

If `clean-transcript` asks whether to run any optional follow-up step, answer "No" and let it finish.

If `clean-transcript` is not installed, write a plain cleaned note in the same shape **without** glossary work, and set `"status": "cleaned-no-glossary"` so it can be reprocessed later.

If one call cannot be cleaned, set `"status": "needs_review"` and a `failure_reason`, then continue. Never halt the whole run for one call.

Write the note before flipping the manifest. One call at a time, oldest first, so the glossary learns in the order the calls happened.

### 4. Refresh the index
Write `meetings/INDEX.md`:

```markdown
# Meeting notes

**Project:** <project> · **Folders:** <folders> · **Total calls:** <N> · **Last updated:** <UTC timestamp>

| Date | Title | Participants | Folder | Note |
|---|---|---|---|---|
| YYYY-MM-DD | <title> | <names> | <folder> | [note](relative/path.md) |
```

Newest first.

### 5. Report
Plain text: `N new · N cleaned · N needs_review`, links to the new notes, and the glossary summary line from each `clean-transcript` run.

## Quality rules

- **No schedule.** A person is present at trigger time. That is also what makes the occasional re-authorisation possible.
- **Atomic per call.** Note first, manifest second.
- **Never invent.** If unsure about participants or context, keep it verbatim.
- **Continue on failure.** One bad call does not stop the rest.
