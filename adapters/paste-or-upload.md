# Adapter: paste or upload (the default)

No connector, no account, no setup. This is how most people should start.

## Option 1: paste

In Claude Code, Cursor, Codex or a chat Project, say:

```
Clean this transcript. Participants: Mira Okafor, Tareq Quillon. Date: 2026-09-08 10:30.

<paste the transcript here>
```

`clean-transcript` takes it from there. The note's frontmatter records `source: paste` and `raw: pasted`.

If you want the raw text kept, ask the agent to save it first to `transcripts/inbox/<YYYY-MM-DD>-<hhmm>-<slug>.txt`. Then `raw:` points at a real file.

## Option 2: drop a file in the inbox

1. Export the transcript from your recording tool.
2. Save it in `transcripts/inbox/`. Name it `<YYYY-MM-DD>-<hhmm>-<anything>.<ext>` so the date is never in doubt.
3. Say: "clean the inbox".

The skill cleans every file in the inbox that does not yet have a note in `meetings/` whose `raw:` points at it. Files are never edited or deleted.

## Formats

| Format | What the skill does |
|---|---|
| `.txt` / `.md` | Reads it as is. Speaker labels like `Name:` or `Speaker 1:` are used for segmentation. |
| `.vtt` (WebVTT) | Drops the `WEBVTT` header, cue numbers and `00:01:02.000 --> 00:01:05.000` lines. Reads speakers from `<v Name>` tags or `Name:` prefixes. Merges consecutive cues from the same speaker. |
| `.srt` (SubRip) | Drops cue numbers and timestamp lines. Reads speakers from `Name:` prefixes if present; otherwise segments by content and keeps generic labels. |

A `.vtt` cue looks like this. Only the speaker and the words are kept:

```
00:04:12.120 --> 00:04:15.900
<v Tareq Quillon>Tareq by here, the trailers are in you no track.
```

## Privacy

`transcripts/inbox/` is in `.gitignore` (except a `.gitkeep`), so raw transcripts stay on your machine unless you choose otherwise. Cleaned notes in `meetings/` are not ignored. Decide per repo whether those belong in git.

## Next

- Pulling calls automatically from a notes app: `adapters/granola/`.
- Otter, Fireflies, Zoom, Teams: `adapters/others.md`.
