# The five guards

A glossary that learns can also learn the wrong thing. Once a wrong row reaches Auto-apply it rewrites every future transcript, quietly. These five guards are how the glossary refuses to poison itself.

## 1. New entries never go straight to Auto-apply

**What it stops:** one confident guess becoming permanent.

A new token enters at Suggest if the context makes its meaning clear, or Watch if it does not. It has to be seen in three distinct transcripts before it replaces anything without a flag.

*Example.* On the first call, "June o truck" could be the in-house app JunoTrack, or a truck booked for June. It enters at Watch. Nothing in the transcript is changed.

## 2. Auto-apply is still context-checked

**What it stops:** a good pattern applied in the wrong sentence.

Even at the top rung, the agent rereads the sentence after a replacement. If the result makes no sense, it puts the raw text back and adds a row to the note's *Contradictions & things to verify* table.

*Example.* "money.com" → Monday.com is Auto-apply in the Banglish pack. In "the money came in on Tuesday", there is no ".com" and no tool. The row does not fire.

## 3. Names are verified against a people source

**What it stops:** invented people.

A name can only enter Category D if the person is listed in the people source (`config/people.md` by default). A name the agent cannot match stays exactly as heard and is flagged as "unverified name".

*Example.* "Tareq by" matches Tareq Quillon in `config/people.md`, once the honorific is split off. "Rumana" is not in the file. She stays "Rumana" in the transcript, flagged, and no Category D row is created.

## 4. You co-own the file

**What it stops:** the agent being the only judge of its own learning.

The glossary is a plain markdown file. Promote, demote or delete any row by hand. The skill is the most frequent writer, not the owner. When you correct a flag in chat ("that was a person, not the tool"), the skill applies your correction and logs it as "(user correction)".

*Example.* You know your team only ever uses Notion, never Motion. Raise the "notion / motion" row from Watch to Suggest yourself and write why in Notes.

## 5. Never silently rewrite

**What it stops:** changes you cannot audit or undo.

Every change (new row, sighting bump, promotion, your own hand edits if you choose to log them) goes into the growth log at the bottom of the glossary. The log is append-only, newest entry on top. The skill never rewords an old row's history; it adds to it.

*Example.*

```markdown
### 2026-09-22 (clean-transcript: Juno Freight dispatch review)
Promoted "you no track / June o truck / juno truck" → JunoTrack from Suggest to Auto-apply:
third distinct transcript. Left one "June truck" verbatim (a truck booked for June, not the app).
```

## What the guards cannot do

They slow mistakes down and make them visible. They do not make the agent right. A wrong row can still reach Auto-apply if the same mishearing is resolved the same wrong way three times and nobody reads the Contradictions table. Read the table. It is short on purpose.
