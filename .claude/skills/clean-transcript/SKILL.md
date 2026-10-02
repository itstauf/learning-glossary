---
name: clean-transcript
description: Glossary-aware cleaning of a raw meeting transcript into a structured note. Loads the learning glossary (paged), segments speakers, reconstructs each turn by confidence tier (Watch, Suggest, Auto-apply), writes the cleaned note with a "Contradictions & things to verify" table, then updates the glossary (new entries, sighting bumps, promotions) and prepends a dated growth-log entry. Sole writer of the glossary. Triggers on "/clean-transcript", "clean transcript", "clean this call", "clean this transcript", "clean the inbox", "tidy this meeting transcript", "glossary-aware cleaning".
---

# clean-transcript

Turns a raw, mis-heard meeting transcript into a clean, structured note, and learns from every run.

It is the **only skill that writes the glossary**. Capture adapters (paste, Granola, Otter, Zoom and the rest) hand it a transcript and step back. The user co-owns the glossary and may edit it by hand at any time.

---

## Configuration

Read `config/clean-transcript.json` if it exists. Every key has a default, so the file is optional.

| Key | Default | What it is |
|---|---|---|
| `glossary_path` | `glossary/glossary.md` | The live glossary this skill reads and writes |
| `glossary_template` | `glossary/glossary.template.md` | Copied to `glossary_path` on first run if no glossary exists |
| `people_path` | `config/people.md` | The people source used to verify names (Category D) |
| `inbox_dir` | `transcripts/inbox` | Where pasted or exported transcripts are dropped |
| `notes_dir` | `meetings` | Where cleaned notes are written |
| `promote_at` | `3` | Distinct transcripts needed to promote Suggest to Auto-apply |
| `page_size` | `200` | Lines per glossary read |

## Inputs

One of:

- a transcript pasted into the chat, plus the participant names if known;
- a file in `inbox_dir`: `.txt`, `.md`, `.vtt` or `.srt`;
- a staged folder from a capture adapter, containing `transcript.md`, optionally `summary.md` and `metadata.json`.

"Clean the inbox" means: every file in `inbox_dir` that no note in `notes_dir` already points at through its `raw:` field, one at a time, oldest first, so the glossary learns in the order the calls happened. Raw files are never edited or deleted.

One meeting recorded by two tools is **one** transcript for counting purposes. Clean the better rendering and count one sighting.

## Outputs

- A cleaned note at `<notes_dir>/<YYYY-MM-DD>-<hhmm>-<slug>.md`. Return the path.
- Glossary changes in `glossary_path`, plus one growth-log entry at the top of the log.
- A short report in chat (Phase 7).

---

## The confidence tiers

**Sightings count distinct transcripts, not occurrences.** Twenty repeats in one call still count as one.

| Tier | Apply behaviour | Moves up when |
|---|---|---|
| **Watch** | Record only. **Never apply.** Leave the raw text as heard. | The context becomes clear enough to say what it means → Suggest |
| **Suggest** | Apply, **and** add a row to the note's *Contradictions & things to verify* table | It is seen in its `promote_at`th distinct transcript (default: the 3rd) → Auto-apply |
| **Auto-apply** | Replace on sight, **still context-checked**. If the replacement would make nonsense, leave the raw text and flag it. | Top tier. Only the user demotes. |

A brand-new pattern enters at **Suggest** when the context is clear, or **Watch** when it is not. Never straight to Auto-apply.

## The five guards

1. New entries never go straight to Auto-apply.
2. Auto-apply is still context-checked. A known pattern that would produce nonsense is flagged, not substituted.
3. Names are verified against the people source (`people_path`). No name enters Category D without a match there.
4. The user co-owns the glossary and may promote, demote or delete any row by hand. This skill is the most frequent writer, not the owner.
5. Never silently rewrite. Every change goes into the append-only growth log, newest on top.

---

## Phases (run in order)

### Phase 1: Intake

- Identify the input. For a staged folder, read `transcript.md`, then `summary.md` and `metadata.json` if present.
- For `.vtt` and `.srt`: drop cue numbers and timestamps, keep speaker labels (`<v Name>` in VTT, `Name:` prefixes in either), and merge consecutive cues from the same speaker into one turn.
- Capture: title, date and start time, participants, source (`paste`, `file`, or the adapter name), and the path of the raw file.
- If the date or participants are missing, ask once. If the user does not know, continue with what you have and write `unknown`.

### Phase 2: Load the glossary (read-only, paged)

- If `glossary_path` does not exist, copy `glossary_template` to it and say so in the report.
- The glossary grows. Do not read it in one go. First locate the sections, for example with `grep -n '^## ' <glossary_path>`, then read in pages with `offset` and `limit` of `page_size` lines.
- The first pages (tier rules, Categories A to C) usually suffice. Read D and E when the call is name-heavy or jargon-heavy.
- Parse each category table into an in-memory lookup: raw variants → resolution, tier, sightings, notes.
- Read `people_path` too. You need it for Phase 3 and for any Category D decision.
- **No writes in this phase.**

### Phase 3: Speaker segmentation

- Split the transcript into speaker turns.
- Map generic labels ("Me:", "Them:", "Speaker 1") to real names only when the metadata or the people source makes it certain. **If unsure, keep the generic label.**
- Split honorifics and terms of address off names (see the pack in use, for example "bhai" or "apa" in the Banglish pack). The honorific is how someone was addressed, not part of their name.

### Phase 4: Reconstruct (apply the glossary)

For every suspicious token, **check the glossary before reconstructing from scratch.** Then act by tier:

- **Auto-apply:** replace. Then reread the sentence. If it now makes no sense, undo it, keep the raw text, add a row to the Contradictions table with "auto-apply failed context check", and do not count a sighting.
- **Suggest:** replace after the same context check, and add a row to the Contradictions table. If the context check fails, keep the raw text and do not count a sighting.
- **Watch:** do not replace on the strength of the glossary. Keep the raw text and note the sighting for Phase 6. One exception: if **this transcript itself** makes the meaning plain (the speaker spells it out, or says what it is), treat the row as Suggest for this call only: apply it, flag it, and move the row to Suggest in Phase 6.
- **Not in the glossary:** if context makes the meaning plain, resolve it, flag it in the Contradictions table, and record it as a candidate new entry (Suggest). If not, keep it verbatim and record it as a candidate Watch entry.

Rules that hold everywhere:

- Change no meaning. Invent nothing. Keep verbatim when unsure.
- A name not found in the people source stays as heard and goes into the Contradictions table as "unverified name".
- Code-switched phrases are translated in the readable transcript only when the glossary says so. Otherwise keep them as spoken.

### Phase 5: Assemble the cleaned note

Write `<notes_dir>/<YYYY-MM-DD>-<hhmm>-<slug>.md`. The slug is the other participants' first names, hyphenated, or a short topic if there are none. Never overwrite an existing note: add `-2` to the slug.

```markdown
---
title: <title>
date: <YYYY-MM-DD HH:MM>
participants: [<names>]
source: <paste | file | granola | otter | ...>
raw: <relative path to the raw transcript, or "pasted">
status: cleaned
cleaned_at: <UTC timestamp>
---

# <title>

> <one-line summary of the call>

**Date:** <human date> · **Participants:** <names>

## Summary
<the capture tool's summary, lightly cleaned; if there is none, a 2 to 3 line synopsis from the transcript>

## Key points & decisions
- <bullets>

## Action items
- [ ] <owner>: <task>
(omit the section if there are none)

## Contradictions & things to verify
| Raw heard | Applied (Suggest) | Why flagged |
|---|---|---|
| <token> | <resolution> | <single source / ambiguous context / unverified name / auto-apply failed context check> |
(omit the section if nothing was flagged)

## Transcript
<a readability pass on the verbatim transcript: real names where known, fillers dropped per Category C, paragraphs. Change no meaning. If unsure, keep verbatim.>
```

### Phase 6: Update the glossary and the growth log (write)

Only after the note is written. Three kinds of change:

1. **New entry.** A token resolved from context that is not in the glossary enters at **Suggest** (or **Watch** if the context was unclear) with `Sightings = 1`, `First seen` and `Last seen` = the call date.
2. **Sighting bump.** A known token seen in this transcript gets `+1`, once per transcript however often it appeared, and `Last seen` = the call date. A new spelling of a known token is added to that row's Raw cell.
3. **Tier change.** Watch → Suggest when this call made the meaning clear. Suggest → Auto-apply when `Sightings` reaches `promote_at`.

Only Category A has Sightings, First seen and Last seen columns. For Categories B to E, keep the count at the start of the Notes cell as `seen N (last YYYY-MM-DD)` and bump it the same way. A row with no count yet (for example one merged from a pack) counts as `seen 0`.

Category D (names) rows are added only when the person is in `people_path`. Fill the People page column with the link to their entry.

Then **prepend** one growth-log entry directly under the `## Growth log` heading:

```markdown
### <YYYY-MM-DD> (clean-transcript: <short call label>)
<one short paragraph: what was added, bumped, promoted or flagged, and why>
```

**Targeted-read-before-edit rule.** A full read of a large glossary truncates, and an edit fails if the exact target lines were not read in this session. So read only the slice you will change (the target row, or the last row of the target table, and the first lines under `## Growth log`) with `offset` and `limit`, then edit. Never edit from memory of a truncated read.

Never delete or reword an existing row's history in this phase. Demotions and deletions are the user's call (guard 4).

### Phase 7: Report

Reply in chat with:

- the path of the cleaned note;
- glossary changes in one line, for example: `2 new (Suggest), 1 new (Watch), 4 bumped, 1 promoted to Auto-apply`;
- every row of the Contradictions table, so the user can confirm or correct;
- anything you could not resolve.

If the user corrects a flag ("no, that was a person, not the tool"), treat it as a hand edit under guard 4: change the row as told and log it in the growth log with "(user correction)".

---

## Contract with other skills

- Capture adapters stage transcripts. They never read or write the glossary.
- An orchestrator (for example `granola-tick`) calls this skill once per staged transcript and reads the returned note path. It never touches the glossary directly.
- See `docs/single-writer.md`.
