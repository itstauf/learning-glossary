# Glossary after call 3 (diff)

What `clean-transcript` changed after cleaning `call-3-raw.md` (2026-09-22). Unchanged rows are not shown. `...` stands for cell text that did not change.

## In one line

`0 new · 8 rows bumped · 1 promoted to Auto-apply (JunoTrack)`

## The rows

```diff
 ## A. Proper nouns (companies, products, tools)
 ...
-| cloud / cloth code / clawed / clawed code | Claude / Claude Code | Auto-apply | pack | 2026-09-08 | 1 | ...
+| cloud / cloth code / clawed / clawed code | Claude / Claude Code | Auto-apply | pack | 2026-09-22 | 2 | ...
-| muddy dot com / muddy.com / mandi.com / money.com | Monday.com | Auto-apply | pack | 2026-09-15 | 2 | ...
+| muddy dot com / muddy.com / mandi.com / money.com | Monday.com | Auto-apply | pack | 2026-09-22 | 3 | ...
-| June o truck / you no track | JunoTrack (Juno Freight's in-house dispatch app) | Suggest | 2026-09-08 | 2026-09-15 | 2 | Call 2: the speaker spelled it ("J U N O... Juno Track, our own dispatch app"). New Suggest entry "you no track" merged with the Watch row "June o truck". Context check: "a truck booked for June" is not this row. |
+| June o truck / you no track / juno truck | JunoTrack (Juno Freight's in-house dispatch app) | Auto-apply | 2026-09-08 | 2026-09-22 | 3 | Call 2: the speaker spelled it ("J U N O... Juno Track, our own dispatch app"). New Suggest entry "you no track" merged with the Watch row "June o truck". Context check: "a truck booked for June" is not this row. PROMOTED Suggest → Auto-apply on 2026-09-22: 3rd distinct transcript. Call 3 also had "the June truck to Chattogram", a real truck: correctly left alone. |

 ## B. Code-switched phrases
 ...
-| Name + "bhai" / "bhaiya" / "by" / "bye" / "buy" fused onto a name | ... | Suggest | seen 1 (last 2026-09-08). ...
+| Name + "bhai" / "bhaiya" / "by" / "bye" / "buy" fused onto a name | ... | Suggest | seen 2 (last 2026-09-22). ...
-| hoye geche / hoy gay chay / hoye gache | "it's done" / "that's sorted" | Suggest | |
+| hoye geche / hoy gay chay / hoye gache | "it's done" / "that's sorted" | Suggest | seen 1 (last 2026-09-22). |
-| shob thik / shob teak / sob thik | "all good" / "everything's fine" | Suggest | |
+| shob thik / shob teak / sob thik | "all good" / "everything's fine" | Suggest | seen 1 (last 2026-09-22). |

 ## C. Fillers & acknowledgements
 ...
-| A lone "4" / "8" / "7" as a whole speaker turn | "Right." / "Mm-hm." | Auto-apply | seen 2 (last 2026-09-15). ...
+| A lone "4" / "8" / "7" as a whole speaker turn | "Right." / "Mm-hm." | Auto-apply | seen 3 (last 2026-09-22). ...

 ## D. Names (verified against the people source, never invented)
 ...
-| tarik / tar egg / Tareq by | Tareq Quillon | config/people.md#tareq-quillon | Suggest | seen 1 (last 2026-09-08). ...
+| tarik / tar egg / Tareq by | Tareq Quillon | config/people.md#tareq-quillon | Suggest | seen 2 (last 2026-09-22). ...

 ## Growth log (append-only, newest on top)

+### 2026-09-22 (clean-transcript: Juno Freight board sync and open claims)
+PROMOTED JunoTrack from Suggest to Auto-apply: third distinct transcript (calls of 08, 15 and 22
+September). Added the spelling "juno truck". Applied it with a flag this one last time, because it
+was still Suggest when the call was cleaned. Left "the June truck to Chattogram" verbatim twice: a
+shipment from June with an open damage claim, not the app. Bumped Claude Code, Monday.com, the bhai
+rule, hoye geche, shob thik, the lone numerals and Tareq. Rumana still not in config/people.md:
+third call in a row. Worth adding her.
+
 ### 2026-09-15 (clean-transcript: Juno Freight dispatch and invoicing sync)
 Moved "June o truck" from Watch to Suggest ...

 ### 2026-09-08 (clean-transcript: Juno Freight yard visibility check-in)
 New Watch row "June o truck": ...
```

## What to look at

- **The promotion happens after the note, not before.** During cleaning, JunoTrack was still Suggest, so call 3's note still flags it. From call 4 on, "juno truck" becomes JunoTrack with no flag.
- **The context check earns its keep.** "The June truck to Chattogram" sounds like the app and is not. It stayed as spoken. At Auto-apply this check keeps running on every call (guard 2).
- **Rumana, three calls running.** The skill will never add her on its own. The growth log now says so plainly. Adding her to `config/people.md` is your call (guards 3 and 4).
- **Monday.com reached 3 local sightings.** It was already Auto-apply from the pack, so nothing changes, but your own evidence now backs it.

Back to `walkthrough.md`.
