# Transcription glossary

> **Writer:** the `clean-transcript` skill is the only skill that writes this file. **You co-own it:** promote, demote or delete any row by hand.
> **Sightings count distinct transcripts, not occurrences.** Twenty repeats in one call still count as one.
> **Growth log:** append-only, newest entry on top.
>
> Copy this file to `glossary/glossary.md` to start (the skill does it for you on first run). To seed it, merge a pack from `packs/`.

---

## Confidence tiers

| Tier | When | Apply behaviour |
|---|---|---|
| **Watch** | Seen, but the meaning is not clear yet | Record only. **Never apply.** |
| **Suggest** | Meaning clear, fewer than 3 distinct transcripts | Apply, **and** flag in the note's *Contradictions & things to verify* table |
| **Auto-apply** | 3 or more distinct transcripts | Replace on sight, still context-checked |

New patterns enter at **Suggest** (or **Watch** if the context is unclear). Never straight to Auto-apply. Promotion to Auto-apply happens at the **3rd distinct transcript**.

## The five guards

1. **No shortcuts.** New entries never go straight to Auto-apply.
2. **Context still wins.** Auto-apply is checked against the sentence. If the replacement makes nonsense, it is flagged, not applied.
3. **No invented people.** Names (Category D) are verified against the people source (`config/people.md` by default).
4. **You co-own it.** Promote, demote or delete rows by hand. The skill is the most frequent writer, not the owner.
5. **Nothing silent.** Every change is recorded in the growth log below, newest on top.

---

## A. Proper nouns (companies, products, tools)

| Raw | Resolves to | Confidence | First seen | Last seen | Sightings | Notes |
|---|---|---|---|---|---|---|

## B. Code-switched phrases

| Raw | Resolves to | Confidence | Notes |
|---|---|---|---|

## C. Fillers & acknowledgements

| Raw | Resolves to | Confidence | Notes |
|---|---|---|---|

## D. Names (verified against the people source, never invented)

| Raw | Person | People page | Confidence | Notes |
|---|---|---|---|---|

## E. Domain jargon

| Raw | Resolves to | Confidence | Notes |
|---|---|---|---|

---

## Growth log (append-only, newest on top)

<!-- clean-transcript prepends entries directly below this line, in this shape:
### YYYY-MM-DD (clean-transcript: short call label)
One short paragraph: what was added, bumped, promoted or flagged, and why.
-->
