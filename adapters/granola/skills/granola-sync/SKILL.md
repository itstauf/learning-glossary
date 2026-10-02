---
name: granola-sync
description: Folder-scoped, verbatim capture of Granola meeting notes into this repo. Pulls only calls filed in the Granola folder(s) named in meetings/.granola/config.json, stages each call (transcript, summary, metadata), and records it in a manifest so nothing is pulled twice. Never cleans and never touches the glossary. Triggers on "sync granola", "pull new calls", "capture new meetings", "any new calls", "fetch transcripts", "/granola-sync".
---

# granola-sync

Verbatim capture. Stages raw files and updates the manifest. Does not clean: run `/granola-tick` for that, or `clean-transcript` on a staged folder.

**Single-writer rule:** this skill never reads or writes the glossary.

## Inputs

- `meetings/.granola/config.json`: `project`, `granola_folders` (array of folder titles), `expected_account`, `staging_dir`, `first_run_start`.
- `meetings/.granola/processed.json`: the manifest.
- A connected Granola MCP server.

## Outputs

- One staged folder per new call under `staging_dir`.
- Updated manifest.
- A short report in chat.

---

## Behaviour (in order)

### 1. Read config and manifest
Read both files. If either is missing, stop and point the user at `adapters/granola/README.md`.

### 2. Connect and check identity
- Find the Granola tools. In Claude Code, search the available tools for "granola". MCP tools are often registered under a session-specific prefix; use whatever prefix you find, never a hardcoded one.
- If the only Granola tool is an authentication tool, run it, give the user the authorisation URL, wait for them to authorise, and complete the flow with the callback URL they paste back.
- Call the account-info tool. Compare the result with `expected_account`. **If it does not match, stop and report which account is connected.** Never capture from the wrong account.
- If `expected_account` still holds its placeholder, stop and ask the user to fill it in.

### 3. Resolve folder IDs (fresh every run)
List the meeting folders. For each title in `granola_folders`, match case-insensitively, ignoring spaces, hyphens and underscores.
- One match: record its title and id.
- No match: list the available folder titles, skip that folder, carry on with the rest.
- Several plausible matches: ask the user to pick. Do not guess.

Resolving by title each run survives folder id changes.

### 4. Discover new meetings
For each resolved folder, list its meetings:
- manifest has meetings: last 30 days;
- manifest empty (first run): custom range from `first_run_start` to today (`date +%Y-%m-%d`).

Diff the returned ids against the manifest keys. Deduplicate across folders. If nothing is new, print `0 new calls in <folders>` and stop.

### 5. Fetch in batches of 10 or fewer
- Get meeting details (title, date, known participants, summary, folder) per batch.
- Get the verbatim transcript per meeting. If the tool saves a large transcript to a file instead of returning it, read that file and extract only the inner transcript string (un-escape `\n` and `\"`). Write the text, not the JSON wrapper.

### 6. Stage each call
Write to `<staging_dir>/<YYYY-MM-DD>-<hhmm>-<slug>-<id8>/`:
- `transcript.md`: verbatim, no edits.
- `summary.md`: verbatim summary. If there is none, write the literal the tool returned (for example `No summary`).
- `metadata.json`: `{ "meeting_id", "title", "date_iso", "date_display", "known_participants", "folder", "fetched_at", "source": "granola-sync" }`.

Naming: `hhmm` is the 24-hour start time; `slug` is the other participants' first names, hyphenated (a solo recording uses a short label from the title); `id8` is the first 8 characters of the meeting id. **Never overwrite** an existing staged folder.

### 7. Update the manifest
Read it, change it in memory, write it back. Per staged call:

```json
{
  "meeting_id": "<id>",
  "title": "<title>",
  "date_iso": "<date>",
  "fetched_at": "<UTC timestamp>",
  "folder": "<folder title>",
  "status": "staged",
  "staged_folder": "meetings/.granola/<folder name>/",
  "cleaned_file": null,
  "cleaned_at": null,
  "failure_reason": null
}
```

Set `last_synced_at` (`date -u +%Y-%m-%dT%H:%M:%SZ`). A failed fetch gets `"status": "failed"` and a `failure_reason`, and is not retried automatically.

### 8. Report
Account, folders resolved, counts (discovered, new, staged, failed), and the staged folder names. Suggest `/granola-tick`. **Stop here. Do not clean.**

## Quality rules

- **Verbatim.** Never edit transcript or summary text.
- **Idempotent.** Skip any id already in the manifest.
- **Atomic per call.** Write all three files before touching the manifest.
- **Never invent participants.** Save `known_participants` exactly as returned, `[]` if none.
- **Folder-scoped.** Ignore every folder not named in config.
- **Silent on no-op.** One line, then stop.
