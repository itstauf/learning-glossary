# Banglish pack

For calls that switch between Bangla and English mid-sentence.

I built this glossary because half my calls do exactly that. A sentence starts in English, picks up a Bangla connector, and ends in English again. Speech-to-text tools are trained on one language at a time, so the Bangla parts come out as English words that sound close: *achha* becomes "4", *mane* becomes "money", a colleague's honorific *bhai* gets fused onto their name as "by". Tool names suffer too: Monday.com came out as "muddy dot com", Claude Code as "cloth code".

This pack is a starting set of those patterns, so your glossary does not begin empty.

## What is in it

| Category | Rows | Examples |
|---|---|---|
| A. Proper nouns | 4 | "cloth code" → Claude Code, "muddy dot com" → Monday.com |
| B. Code-switched phrases | 10 | *ki bolbo* → "what can I say", the *bhai* / *apa* honorific rule, *mane* → "I mean" |
| C. Fillers & acknowledgements | 5 | a lone "4" / "8" / "7" on a turn → "Right." / "Mm-hm." |
| D. Names | 3 | fictional examples only (Mira Okafor, Nilu Fernhall, Tareq Quillon) |
| E. Domain jargon | 2 | "el see" → LC (letter of credit) |

The four Auto-apply rows (Claude / Claude Code, Monday.com, the lone numerals, a standalone *accha*) are patterns I saw across many of my own calls. Everything else is a synthetic but realistic example, set to Suggest or Watch.

## The honorific rule

The most useful row in the pack is a rule, not a word swap. In Bangla you address an older or respected colleague as *Name bhai* (brother) or *Name apa* (sister). Transcription tools glue the honorific onto the name: "Tareq by", "Nilu upper". Left alone, the glossary would one day learn a person called "Tareq By".

So the rule says: split the honorific off. The transcript keeps "Tareq bhai said...", because that is how he was addressed. The participants list and Category D use the bare name, "Tareq".

## How to install

1. Make sure `glossary/glossary.md` exists (copy `glossary/glossary.template.md`, or run `clean-transcript` once).
2. For each category, copy the rows you want from `pack.md` into the matching table in your glossary.
3. Delete the fictional Category D rows. Add your real colleagues to `config/people.md` instead and let the skill learn how their names get misheard.
4. Add one growth-log entry at the top of the log, for example:
   `### 2026-10-03 (user: merged Banglish pack)` with one line saying which rows you took.

Or ask your agent: "Merge the Banglish pack into my glossary, skip Category D, and log it." That is a hand edit you asked for, so it sits under guard 4 (you co-own the file).

## Why some pack rows start at Auto-apply

Guard 1 says new entries never go straight to Auto-apply. That guard is about the skill: it may not promote something on one sighting. A pack is different. It is evidence I already collected, imported by you, on purpose. If you would rather your own calls earn every row, change the Confidence cell to Suggest before you merge. Three of your calls later, the ladder will have done it anyway.

## Contributing

Seen a pattern that belongs here? Open an issue with the "idea" template: the raw text, what it should resolve to, and one synthetic sentence that shows the context. Never paste a real transcript.
