# Adapter: Otter, Fireflies, Zoom, Teams and other exports

You do not need a connector for these. Export a file, drop it in `transcripts/inbox/`, and say "clean the inbox". The paste-or-upload adapter (`adapters/paste-or-upload.md`) does the rest.

Prefer `.vtt` when the tool offers it. It keeps speaker names, which saves the skill from guessing who said what.

| Tool | Where the export usually lives | Best format |
|---|---|---|
| Zoom (cloud recording) | Recordings → the meeting → the audio transcript file | `.vtt` |
| Microsoft Teams | The meeting chat or recap → Transcript → Download | `.vtt` (or `.docx`; save it as `.txt`) |
| Google Meet | The transcript document saved to Drive after the call | export the doc as `.txt` |
| Otter | The conversation → Export → Text | `.txt` with speaker names on, or `.srt` |
| Fireflies | The meeting → Download → Transcript | `.vtt` or `.srt` |

Menus move between versions. If the path above has changed, look for "Transcript" and "Download" or "Export" on the meeting's page.

## Naming

Rename each file `<YYYY-MM-DD>-<hhmm>-<short-label>.<ext>`, for example `2026-09-15-1400-dispatch-review.vtt`. The skill takes the date from the file name when the transcript itself does not carry one.

## Two tools on the same call

Some people record a call in two tools at once. Each tool mishears differently, which is useful evidence. But it is still one call. Clean the better transcript, and mention the other in the note's summary if it resolves something. **It counts as one sighting, not two.** Two renderings of one meeting are one transcript for the ladder.

## Want it automatic?

Write a capture adapter for your tool the way `adapters/granola/` does it: stage verbatim files plus a manifest, then call `clean-transcript` once per new call. Keep to the single-writer rule (`docs/single-writer.md`): the adapter never touches the glossary.
