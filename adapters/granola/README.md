# Adapter: Granola (folder-scoped, manual trigger)

For people who already take call notes in Granola. Each repo captures only the calls you filed in one Granola folder, and only when you ask.

This is the night-shift part of the series: capture that runs while you get on with your day. Chapter: [The night shift](https://itstauf.com/resources/second-brain/night-shift?utm_source=github&utm_medium=readme&utm_campaign=compounding-brain&utm_content=learning-glossary).

## How it fits

```
you type /granola-tick
        │
        ▼
  granola-sync ──▶ list the folder named in config ──▶ pull only NEW calls ──▶ stage verbatim
        │                                                                       meetings/.granola/<call>/
        ▼
  clean-transcript, once per new call (the only glossary writer)
        │
        ▼
  meetings/<date>-<hhmm>-<slug>.md  +  meetings/INDEX.md  ──▶  report in chat
```

Two skills, two jobs:

- **granola-sync** pulls and stages. Verbatim. Keeps a manifest so nothing is pulled twice.
- **granola-tick** runs sync, then hands each new call to `clean-transcript`, then refreshes the index.

Neither touches the glossary. See `docs/single-writer.md`.

## Prerequisites

1. **The Granola MCP server connected** in your agent. The first use may ask you to authorise in a browser and paste a callback URL back.
2. **A Granola folder for this project.** Capture only sees calls inside it. File calls there by hand or with Granola's folder rules.
3. **You, present when it runs.** It is manual on purpose: authorisation sometimes needs a human, and you should see what got pulled.

## Install (Claude Code)

From the repo root:

```bash
mkdir -p .claude/skills meetings/.granola
cp -r adapters/granola/skills/granola-sync .claude/skills/
cp -r adapters/granola/skills/granola-tick .claude/skills/
cp adapters/granola/config.json    meetings/.granola/config.json
cp adapters/granola/processed.json meetings/.granola/processed.json
```

Then edit `meetings/.granola/config.json`:

| Key | Set it to |
|---|---|
| `project` | a short name for this repo |
| `granola_folders` | the exact title(s) of your Granola folder(s), as an array |
| `expected_account` | the Granola login you expect to be connected. The sync stops if a different account answers. This stops a personal account's calls landing in a work repo, or the other way round. |
| `output_dir` | where cleaned notes go (default `meetings`) |
| `first_run_start` | how far back the first run looks (default `2024-01-01`) |

Copy the same project name and folder titles into `meetings/.granola/processed.json`.

## Run it

- Capture and clean: `/granola-tick`, or "catch up on meetings".
- Capture only: `/granola-sync`.

No interval, no routine. It runs when you ask.

## Notes

- **The first run pulls history** back to `first_run_start`. It fetches in batches of 10 and is idempotent: if it stops halfway, run it again and it resumes.
- **Only an authentication tool shows up.** The real tools appear after you authorise. Follow the prompt and paste the callback URL back.
- **"No folder match".** Rename the folder in Granola or fix `granola_folders` in config.
- **Wrong account.** Reconnect the right Granola account, or correct `expected_account` if you changed logins on purpose.
- **Git.** `.gitignore` excludes the staged raw folders (`meetings/.granola/*/`) by default. Commit `config.json` and `processed.json` if you want sync state to travel with the repo; commit `meetings/*.md` if you want the notes in git.
- **Time zone.** Timestamps are UTC. Change the `date -u` calls in the skills if you want a fixed offset.

## Other tools

Not on Granola? Use `adapters/paste-or-upload.md` or `adapters/others.md`. Same skill, same glossary, no connector.
