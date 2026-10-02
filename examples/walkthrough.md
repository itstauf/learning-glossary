# Walkthrough: one word climbs the ladder

Three short synthetic calls at a fictional company, Juno Freight. Everyone in them is fictional. Follow one entry, the in-house dispatch app **JunoTrack**, from a mishearing nobody can place to a pattern the glossary applies on sight.

Before call 1 the glossary is `glossary/glossary.template.md` with the Banglish pack (`packs/banglish/pack.md`) merged in. The three fictional people in `config/people.md` are the people source.

## The climb at a glance

| | Call 1 · 8 Sep | Call 2 · 15 Sep | Call 3 · 22 Sep | Call 4 onwards |
|---|---|---|---|---|
| Heard as | "June o truck" (x3) | "you no track" (x3), "June o truck" (x1) | "juno truck" (x2), plus a real "June truck" (x2) | any of the above |
| Tier while cleaning | not in glossary | **Watch** | **Suggest** | **Auto-apply** |
| What the note shows | raw text, untouched | JunoTrack, **flagged** | JunoTrack, **flagged**; the real "June truck" untouched | JunoTrack, no flag; still context-checked |
| Sightings after | 1 | 2 | 3 | 4, 5, ... |
| Tier after | **Watch** | **Suggest** | **Auto-apply** | Auto-apply |

```
 call 1                      call 2                         call 3
 "June o truck"              "you no track"                 "juno truck"
 meaning unclear      ──▶    speaker spells it:      ──▶    3rd distinct transcript
 WATCH, 1 sighting           J-U-N-O, "our own app"         SUGGEST → AUTO-APPLY
 (nothing applied)           SUGGEST, 2 sightings           (flagged one last time)
                             (applied + flagged)
```

## Call 1: Watch

Files: `call-1-raw.md` → `call-1-cleaned.md`, changes in `glossary-after-call-1.md`.

Tareq says the dispatch team is "putting it in June o truck now... the new one". Mira asks "June what?" and gets the same words back. The skill checks the glossary: nothing. Can it resolve the token from context? Not safely. It might be a tool. It might be a truck booked for June.

So it does the honest thing. It leaves "June o truck" in the cleaned transcript exactly as heard, and adds a **Watch** row with one sighting. Three mentions, one sighting: one call proves nothing about what a word means.

Meanwhile the pack does its job on everything else. "muddy dot com" becomes Monday.com and "cloth code" becomes Claude Code (Auto-apply, no flag). The lone "4" and "7" turns become "Right." and "Mm-hm.". "Tareq by" becomes "Tareq bhai", with the honorific split off his name; that one is Suggest, so it shows up in the note's **Contradictions & things to verify** table, alongside WhatsApp, *ki bolbo*, *mane* and *tai na*. And "Rumana", who is not in `config/people.md`, stays "Rumana" and is flagged. No person is invented.

## Call 2: Suggest, and the first flag

Files: `call-2-raw.md` → `call-2-cleaned.md`, changes in `glossary-after-call-2.md`.

The ASR now hears "you no track". Mira asks Tareq to spell it. He does: "J U N O. Juno, like the company. Juno Track. Our own dispatch app."

The row is Watch, and Watch rows are never applied from the glossary. But this transcript itself settles the meaning. So for this one call the skill treats the row as Suggest: it writes JunoTrack in the transcript and adds a row to the Contradictions table:

| Raw heard | Applied (Suggest) | Why flagged |
|---|---|---|
| you no track / June o truck | JunoTrack | Was Watch. The speaker spelled it out in this call ("J U N O... Juno Track"), so applied for this call and moved to Suggest |

After the note is written, the glossary row moves to **Suggest**, gains the spelling "you no track", and goes to 2 sightings. Four mishearings in this call, still +1.

Two other things worth seeing in call 2:

- **Guard 2 in action.** Nilu keeps invoices "on the cloud drive". "cloud" is an Auto-apply raw form of Claude. The skill applies it, rereads the sentence, sees nonsense, puts "cloud" back and flags the decision. No sighting is counted.
- **Generic labels stay generic.** Three people, two labels. Where the skill cannot tell whether "Them" is Tareq or Nilu, it writes "Them" and says so.

## Call 3: Auto-apply

Files: `call-3-raw.md` → `call-3-cleaned.md`, changes in `glossary-after-call-3.md`.

A third spelling: "juno truck". The row is Suggest, so the skill applies JunoTrack and flags it, one last time.

Then a trap. Mira mentions "the June truck to Chattogram", and Tareq says "the June truck, that one has a damage claim still open". This is a real truck from June. The skill reads the sentence, not just the token, and leaves it alone. The Contradictions table records the decision so you can check it.

After the note is written: 3 distinct transcripts. The row is **promoted to Auto-apply**, and the growth log says so at the top:

```markdown
### 2026-09-22 (clean-transcript: Juno Freight board sync and open claims)
PROMOTED JunoTrack from Suggest to Auto-apply: third distinct transcript (calls of 08, 15 and 22
September). ...
```

## Call 4 and after

"juno truck", "you no track" and "June o truck" become JunoTrack with no flag. The context check keeps running: the next "June truck" that really is a June truck stays a June truck. If the glossary ever gets it wrong, you can demote the row by hand (guard 4), and the growth log shows exactly when and why it climbed (guard 5).

## Try it yourself

1. Copy `glossary/glossary.template.md` to `glossary/glossary.md` and merge `packs/banglish/pack.md`.
2. Paste `call-1-raw.md` into your agent and say "clean this transcript".
3. Compare your note and glossary diff with the files here. Then do calls 2 and 3.

Your agent's wording will differ. The tiers, the sighting counts and the flags should not.
