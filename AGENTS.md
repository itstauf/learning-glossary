# AGENTS.md

Instructions for any coding agent working in this repo (Codex, Cursor, Claude Code, Copilot, Aider and others).

## What this repo is

A procedure for cleaning meeting transcripts and a glossary that learns the user's words. There is no code to build or run. The "program" is a markdown skill your agent follows.

## The one file to follow

`.claude/skills/clean-transcript/SKILL.md`

When the user says "clean this transcript", "clean this call", "clean the inbox" or similar, follow that file's seven phases in order: intake, load the glossary (paged), speaker segmentation, reconstruct by tier, assemble the note, update the glossary and growth log, report. The path says `.claude`, but nothing in it is specific to one agent.

## Files you read

| File | Why |
|---|---|
| `config/clean-transcript.json` | Paths and settings. Every key has a default. |
| `glossary/glossary.md` | The live glossary. If missing, copy `glossary/glossary.template.md` to it. |
| `config/people.md` | The people source. Names are only added to the glossary if listed here. |
| `transcripts/inbox/` | Raw transcripts dropped by the user (`.txt`, `.md`, `.vtt`, `.srt`). |
| `packs/*/pack.md` | Optional seed rows. Merge only when the user asks. |

## Files you write

| File | When |
|---|---|
| `meetings/<YYYY-MM-DD>-<hhmm>-<slug>.md` | One cleaned note per transcript. Never overwrite. |
| `glossary/glossary.md` | Only while running the clean-transcript procedure, or when the user explicitly asks for a hand edit or a pack merge. |

## Hard rules

1. **Single writer.** Only the clean-transcript procedure writes the glossary. Capture adapters (`adapters/`) never touch it. See `docs/single-writer.md`.
2. **Sightings count distinct transcripts.** Twenty repeats in one call count as one.
3. **New entries never go straight to Auto-apply.** Suggest if the context is clear, Watch if not. Auto-apply at the 3rd distinct transcript.
4. **Auto-apply is still context-checked.** If the replacement makes nonsense, keep the raw text and flag it.
5. **Never invent a person.** Category D needs a match in the people source.
6. **Never silently rewrite.** Every glossary change gets a growth-log entry, newest on top. Never demote or delete a row unless the user asks.
7. **Targeted read before edit.** The glossary grows large. Read it in pages (`offset` / `limit`), and before each edit read the exact slice you will change.
8. **Raw is read-only.** Never edit or delete files in `transcripts/inbox/` or staged capture folders.

## Optional adapters

`adapters/granola/` holds two extra skills (`granola-sync`, `granola-tick`) and an install guide. They are not active until the user copies them into place and fills in `meetings/.granola/config.json`. Never run them on a schedule.

## Examples

`examples/walkthrough.md` shows the expected behaviour on three synthetic calls. If your output disagrees with it on tiers, sighting counts or flags, the walkthrough is right.
