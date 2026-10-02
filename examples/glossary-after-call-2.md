# Glossary after call 2 (diff)

What `clean-transcript` changed after cleaning `call-2-raw.md` (2026-09-15). Unchanged rows are not shown. `...` stands for cell text that did not change.

## In one line

`1 moved Watch → Suggest · 5 rows bumped · 0 promoted · 1 Auto-apply held back by the context check`

## The rows

```diff
 ## A. Proper nouns (companies, products, tools)
 ...
-| muddy dot com / muddy.com / mandi.com / money.com | Monday.com | Auto-apply | pack | 2026-09-08 | 1 | ...
+| muddy dot com / muddy.com / mandi.com / money.com | Monday.com | Auto-apply | pack | 2026-09-15 | 2 | ...
-| June o truck | _(unresolved: probably a new dispatch tool, spelling unknown)_ | Watch | 2026-09-08 | 2026-09-08 | 1 | "Dispatch is putting it in June o truck now... the new one." Could also be a truck booked for June. Said 3 times, counted once. Do not apply. |
+| June o truck / you no track | JunoTrack (Juno Freight's in-house dispatch app) | Suggest | 2026-09-08 | 2026-09-15 | 2 | Call 2: the speaker spelled it ("J U N O... Juno Track, our own dispatch app"). Moved up from Watch. Context check: "a truck booked for June" is not this row. |

 ## B. Code-switched phrases
 ...
-| Name + "apa" / "apu" / "appa" / "upper" fused onto a name | ... | Suggest | seen 1 (last 2026-09-08). ...
+| Name + "apa" / "apu" / "appa" / "upper" fused onto a name | ... | Suggest | seen 2 (last 2026-09-15). ...

 ## C. Fillers & acknowledgements
 ...
-| A lone "4" / "8" / "7" as a whole speaker turn | "Right." / "Mm-hm." | Auto-apply | seen 1 (last 2026-09-08). ...
+| A lone "4" / "8" / "7" as a whole speaker turn | "Right." / "Mm-hm." | Auto-apply | seen 2 (last 2026-09-15). ...
-| accha / acha / atta / attach / "at the" (as an acknowledgement) | "Okay." / "Right." | Auto-apply | seen 1 (last 2026-09-08). ...
+| accha / acha / atta / attach / "at the" (as an acknowledgement) | "Okay." / "Right." | Auto-apply | seen 2 (last 2026-09-15). ...

 ## D. Names (verified against the people source, never invented)
 ...
-| new loo / nil u / Nilu upper | Nilu Fernhall | config/people.md#nilu-fernhall | Suggest | seen 1 (last 2026-09-08). ...
+| new loo / nil u / Nilu upper | Nilu Fernhall | config/people.md#nilu-fernhall | Suggest | seen 2 (last 2026-09-15). ...

 ## Growth log (append-only, newest on top)

+### 2026-09-15 (clean-transcript: Juno Freight dispatch and invoicing sync)
+Moved "June o truck" from Watch to Suggest and added the spelling "you no track": Tareq spelled the
+name in this call (JunoTrack, the in-house dispatch app). Misheard 4 times across two spellings,
+counted once: 2 distinct transcripts. Bumped Monday.com, the apa rule, Nilu, the lone numerals
+and accha. Held back Claude / Claude Code on "the cloud drive" (file storage, not the assistant);
+no bump. Did not apply mane to "the money from two carriers" (literal money); no bump. Rumana
+still not in config/people.md.
+
 ### 2026-09-08 (clean-transcript: Juno Freight yard visibility check-in)
 New Watch row "June o truck": ...
```

## What to look at

- **The climb.** "June o truck" was Watch. This call made it plain, so it was applied in this note *with a flag* and moved to Suggest. It now has 2 sightings: call 1 and call 2. The four mishearings in call 2 count as one.
- **A held-back Auto-apply.** "cloud" → Claude is Auto-apply, but "the cloud drive" is file storage. The context check kept "cloud" and put a row in the Contradictions table so you can see the decision. That is guard 2.
- **A literal word.** "money" is a raw form of *mane* ("I mean"), but "the money from two carriers came in late" is money. Not applied, not counted.
- **Rows that did not fire are not touched.** Most of the glossary is unchanged.
- **Newest on top.** The new log entry sits above call 1's.

Next: `call-3-raw.md`.
