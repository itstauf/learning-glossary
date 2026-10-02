# Glossary after call 1 (diff)

What `clean-transcript` changed in `glossary/glossary.md` after cleaning `call-1-raw.md` (2026-09-08). Unchanged rows are not shown. Lines starting `-` were removed, `+` added.

## In one line

`1 new (Watch) · 12 rows bumped · 0 promoted · 1 unverified name flagged (no row created)`

## The rows

```diff
 ## A. Proper nouns (companies, products, tools)

 | Raw | Resolves to | Confidence | First seen | Last seen | Sightings | Notes |
 |---|---|---|---|---|---|---|
-| cloud / cloth code / clawed / clawed code | Claude / Claude Code | Auto-apply | pack | pack | 0 (pack) | Context check: "the cloud" meaning hosting stays "cloud". Apply when an AI assistant or coding tool is meant. |
+| cloud / cloth code / clawed / clawed code | Claude / Claude Code | Auto-apply | pack | 2026-09-08 | 1 | Context check: "the cloud" meaning hosting stays "cloud". Apply when an AI assistant or coding tool is meant. |
-| muddy dot com / muddy.com / mandi.com / money.com | Monday.com | Auto-apply | pack | pack | 0 (pack) | Work-management tool. Context check: "money" on its own is not this row. |
+| muddy dot com / muddy.com / mandi.com / money.com | Monday.com | Auto-apply | pack | 2026-09-08 | 1 | Work-management tool. Context check: "money" on its own is not this row. |
-| what's up / whats app (as a channel) | WhatsApp | Suggest | pack | pack | 0 (pack) | Only when it names the channel ("send it on what's up"). A greeting stays a greeting. |
+| what's up / whats app (as a channel) | WhatsApp | Suggest | pack | 2026-09-08 | 1 | Only when it names the channel ("send it on what's up"). A greeting stays a greeting. |
+| June o truck | _(unresolved: probably a new dispatch tool, spelling unknown)_ | Watch | 2026-09-08 | 2026-09-08 | 1 | "Dispatch is putting it in June o truck now... the new one." Could also be a truck booked for June. Said 3 times, counted once. Do not apply. |

 ## B. Code-switched phrases
 ...
-| Name + "bhai" / "bhaiya" / "by" / "bye" / "buy" fused onto a name | ... | Suggest | Rule, not a word swap. ...
+| Name + "bhai" / "bhaiya" / "by" / "bye" / "buy" fused onto a name | ... | Suggest | seen 1 (last 2026-09-08). Rule, not a word swap. ... "Thank you, bye" at the end of call 1 correctly left alone.
-| Name + "apa" / "apu" / "appa" / "upper" fused onto a name | ... | Suggest | "Nilu upper sent it" ...
+| Name + "apa" / "apu" / "appa" / "upper" fused onto a name | ... | Suggest | seen 1 (last 2026-09-08). "Nilu upper sent it" ...
-| ki bolbo / key bowl bow / kee bolbo | "what can I say" | Suggest | Usually a shrug ...
+| ki bolbo / key bowl bow / kee bolbo | "what can I say" | Suggest | seen 1 (last 2026-09-08). Usually a shrug ...
-| mane / maane / "money" mid-sentence | "I mean" / "that is" (a clarifying connector) | Suggest | Context check is essential ...
+| mane / maane / "money" mid-sentence | "I mean" / "that is" (a clarifying connector) | Suggest | seen 1 (last 2026-09-08). Context check is essential ...
-| tai na / tie na / tay na | "isn't it?" / "right?" (tag question) | Suggest | Sits at the end ...
+| tai na / tie na / tay na | "isn't it?" / "right?" (tag question) | Suggest | seen 1 (last 2026-09-08). Sits at the end ...

 ## C. Fillers & acknowledgements
 ...
-| A lone "4" / "8" / "7" as a whole speaker turn | "Right." / "Mm-hm." | Auto-apply | ASR rendering ...
+| A lone "4" / "8" / "7" as a whole speaker turn | "Right." / "Mm-hm." | Auto-apply | seen 1 (last 2026-09-08). ASR rendering ...
-| accha / acha / atta / attach / "at the" (as an acknowledgement) | "Okay." / "Right." | Auto-apply | Bangla *achha* ...
+| accha / acha / atta / attach / "at the" (as an acknowledgement) | "Okay." / "Right." | Auto-apply | seen 1 (last 2026-09-08). Bangla *achha* ...

 ## D. Names (verified against the people source, never invented)
 ...
-| new loo / nil u / Nilu upper | Nilu Fernhall | config/people.md#nilu-fernhall | Suggest | "upper" is the honorific ...
+| new loo / nil u / Nilu upper | Nilu Fernhall | config/people.md#nilu-fernhall | Suggest | seen 1 (last 2026-09-08). "upper" is the honorific ...
-| tarik / tar egg / Tareq by | Tareq Quillon | config/people.md#tareq-quillon | Suggest | "by" is the honorific ...
+| tarik / tar egg / Tareq by | Tareq Quillon | config/people.md#tareq-quillon | Suggest | seen 1 (last 2026-09-08). "by" is the honorific ...

 ## Growth log (append-only, newest on top)

+### 2026-09-08 (clean-transcript: Juno Freight yard visibility check-in)
+New Watch row "June o truck": sounds like a new dispatch tool, but the call never says what it is
+called or how it is spelled, and "a truck booked for June" also fits. Not applied. Bumped 12 rows
+once each (Claude Code, Monday.com, WhatsApp, the bhai and apa rules, ki bolbo, mane, tai na, the
+lone numerals, accha, Nilu, Tareq). "Rumana" is not in config/people.md: kept as heard, flagged in
+the note, no Category D row created.
```

`...` stands for cell text that did not change. The real file holds the full row.

## Why no row climbed

Every bump took a row from `seen 0` to `seen 1`. Pack rows start your own count at zero, so even the Auto-apply ones are only at 1 sighting in *your* calls. Nothing is near the promotion line yet.

## What to look at

- **The Watch row.** "June o truck" was heard three times in this call. It is still one sighting. One call proves nothing about what a token means.
- **Rumana.** The skill did not invent "Rumana ..." as a person. If she is real, add her to `config/people.md` and the next call can create her row.
- **The Monday.com row** fired twice in the call and was bumped once.

Next: `call-2-raw.md`.
