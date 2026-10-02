# Banglish pack (Bangla-English code-switching)

Seed rows for people whose calls switch between Bangla and English mid-sentence. Merge the rows you want into your own `glossary/glossary.md`, category by category. See `README.md` in this folder.

Every Category D row is an obviously fictional example. Delete them and add your own people through `config/people.md`.

`Sightings` reads `0 (pack)`: your own count starts at zero. The tier is the one the pattern earned on the author's calls, or a suggested tier for synthetic rows. Set any row to Suggest if you want your own calls to earn it.

---

## A. Proper nouns (companies, products, tools)

| Raw | Resolves to | Confidence | First seen | Last seen | Sightings | Notes |
|---|---|---|---|---|---|---|
| cloud / cloth code / clawed / clawed code | Claude / Claude Code | Auto-apply | pack | pack | 0 (pack) | Context check: "the cloud" meaning hosting stays "cloud". Apply when an AI assistant or coding tool is meant. |
| muddy dot com / muddy.com / mandi.com / money.com | Monday.com | Auto-apply | pack | pack | 0 (pack) | Work-management tool. Context check: "money" on its own is not this row. |
| what's up / whats app (as a channel) | WhatsApp | Suggest | pack | pack | 0 (pack) | Only when it names the channel ("send it on what's up"). A greeting stays a greeting. |
| bee cash / bekash | bKash | Suggest | pack | pack | 0 (pack) | Mobile payments app. Apply only in a payments context. |

## B. Code-switched phrases

| Raw | Resolves to | Confidence | Notes |
|---|---|---|---|
| Name + "bhai" / "bhaiya" / "by" / "bye" / "buy" fused onto a name | Honorific *bhai* ("brother"), a term of address. **Split it off the name.** | Suggest | Rule, not a word swap. "Tareq by said" → "Tareq bhai said". Participants list and Category D use the bare name ("Tareq"). Never create a person called "Tareq By". Context check: "Thank you, bye" at the end of a call is a goodbye. |
| Name + "apa" / "apu" / "appa" / "upper" fused onto a name | Honorific *apa* / *apu* ("sister"), the female counterpart of the rule above. **Split it off the name.** | Suggest | "Nilu upper sent it" → "Nilu apa sent it". The name is "Nilu". |
| ki bolbo / key bowl bow / kee bolbo | "what can I say" | Suggest | Usually a shrug before a hard admission. Keep the Bangla in the transcript if you prefer, with the gloss once. |
| mane / maane / "money" mid-sentence | "I mean" / "that is" (a clarifying connector) | Suggest | Context check is essential: "money, the deadline moved" is *mane*; "the money came in" is money. |
| kintu / gintu / kin to | "but" | Watch | Often mis-rendered as a name. Recorded so it is never read as a person. Do not apply until your own calls make the pattern clear. |
| tai na / tie na / tay na | "isn't it?" / "right?" (tag question) | Suggest | Sits at the end of a sentence. Render as ", right?" |
| shob thik / shob teak / sob thik | "all good" / "everything's fine" | Suggest | |
| hoye geche / hoy gay chay / hoye gache | "it's done" / "that's sorted" | Suggest | |
| inshallah / in sha allah / insha'allah | Keep as spoken. Gloss once as "God willing". | Suggest | A hedge on a future commitment. Do not translate it away; it carries meaning about certainty. |
| _(Bangla rendered in Devanagari or another wrong script)_ | **Not resolvable. Leave verbatim and flag.** | Watch | Some tools render Bangla in the wrong script and break words mid-way. Never guess a translation from it. |

## C. Fillers & acknowledgements

| Raw | Resolves to | Confidence | Notes |
|---|---|---|---|
| A lone "4" / "8" / "7" as a whole speaker turn | "Right." / "Mm-hm." | Auto-apply | ASR rendering of Bangla *achha* / *ji* / *mm*. Only when the numeral is the entire turn. A number inside a sentence is a number. |
| accha / acha / atta / attach / "at the" (as an acknowledgement) | "Okay." / "Right." | Auto-apply | Bangla *achha*, an acknowledgement. Only when it stands alone, or opens or closes a turn. |
| ji / gee / "G" (alone on a turn) | "Yes." | Suggest | Polite yes. |
| hmm haan / hum han | "Mm, yes." | Suggest | |
| thik ache / tick a chay / theek ache | "Okay." / "Fine." | Suggest | Agreement, sometimes mid-turn. |

## D. Names (verified against the people source, never invented)

Fictional examples. Delete before real use.

| Raw | Person | People page | Confidence | Notes |
|---|---|---|---|---|
| mirror / Mira OK for / meera | Mira Okafor | config/people.md#mira-okafor | Suggest | Context check: "mirror" as an object stays. |
| new loo / nil u / Nilu upper | Nilu Fernhall | config/people.md#nilu-fernhall | Suggest | "upper" is the honorific *apa*; split it off (Category B). |
| tarik / tar egg / Tareq by | Tareq Quillon | config/people.md#tareq-quillon | Suggest | "by" is the honorific *bhai*; split it off (Category B). |

## E. Domain jargon

| Raw | Resolves to | Confidence | Notes |
|---|---|---|---|
| el see / L.C. / elsie | LC (letter of credit) | Suggest | Trade and import calls. Context check: "Elsie" may be a person; check the people source. |
| challan / chalan / shallon | Challan (delivery or deposit slip) | Suggest | Keep the word; gloss once. |
