# The single-writer rule

**Only `clean-transcript` writes the glossary.** You can edit it by hand too, because you co-own it. Nothing else touches it.

## Why

Capture and learning are different jobs. Capture is about getting the raw words in, untouched. Learning is about deciding what those words meant. If a capture adapter also edited the glossary, you would have two places deciding what is true, and their rules would drift.

With one writer:

- every glossary change goes through the same tier rules and the same five guards;
- every change lands in the same growth log;
- you can swap or add capture tools without touching the learning loop.

## Who does what

```
  capture adapters                   the learner                    the store
 ┌────────────────────┐          ┌────────────────────┐        ┌──────────────────────┐
 │ paste-or-upload    │          │                    │  R/W   │ glossary/glossary.md │
 │ granola-sync       │ ──raw──▶ │  clean-transcript  │ ─────▶ │ (+ growth log)       │
 │ Otter/Zoom/Teams   │          │                    │        └──────────────────────┘
 │ exports (.vtt)     │          └─────────┬──────────┘
 └────────────────────┘                    │ writes
          │ writes                         ▼
          ▼                      meetings/<date>-<hhmm>-<slug>.md
  staged raw files + a manifest
  (never the glossary)
```

| Component | Reads the glossary? | Writes the glossary? |
|---|:---:|:---:|
| `clean-transcript` | yes | **yes, the only skill that does** |
| an orchestrator such as `granola-tick` | no | no. It calls `clean-transcript` once per transcript and reads back the note path. |
| a capture adapter such as `granola-sync` | no | no. It stages verbatim files and keeps its own manifest. |
| you | yes | yes, by hand (guard 4) |

Two stores, never conflated:

- **The glossary** is the learning loop. Owner: `clean-transcript`.
- **A capture manifest** (for example `meetings/.granola/processed.json`) records which calls have been pulled and cleaned. Owner: the adapter.

## Hand edits and pack merges

When you edit the glossary yourself, or ask your agent to merge a pack, that is you exercising guard 4. It is allowed. Log it in the growth log with "(user: ...)" in the heading so the history stays complete.

What is not allowed: a capture skill that "helpfully" adds a row because it noticed something. If an adapter sees a pattern, it belongs in the transcript it stages, for `clean-transcript` to judge.

## The targeted-read-before-edit rule

The glossary grows. After a few months mine was over a thousand lines. Two things follow:

1. **Load it in pages.** Find the section headings first (`grep -n '^## '`), then read with `offset` and `limit`. Read only the categories the call needs.
2. **Read the exact slice before you edit it.** Many agent tools refuse an edit to lines they have not read in the current session, and a full read of a large file is silently truncated. So before each write, read the target row (or the last row of the target table) and the first lines under `## Growth log`, then edit. Never edit from memory of a truncated read.

The first time I skipped this, the edit failed with "file has not been read yet". The rule exists because of that failure.
