# English pack (tools, jargon, fillers)

Seed rows for English-language calls about software, AI and operations. Merge the rows you want into your own `glossary/glossary.md`. See `README.md` in this folder.

`Sightings` reads `0 (pack)`: your own count starts at zero. Tiers are suggestions. Rows where both sides are real words or real products sit at Watch or Suggest on purpose.

---

## A. Proper nouns (companies, products, tools)

| Raw | Resolves to | Confidence | First seen | Last seen | Sightings | Notes |
|---|---|---|---|---|---|---|
| cloud code / clawed code / cloth code / clod code | Claude Code | Auto-apply | pack | pack | 0 (pack) | "Code" next to it makes this safe. A bare "cloud" is not this row. |
| clawed / claud (as an assistant) | Claude | Suggest | pack | pack | 0 (pack) | Context check: "the cloud" meaning hosting stays "cloud". |
| chat GBT / chat GPT / chat GP | ChatGPT | Auto-apply | pack | pack | 0 (pack) | |
| open AI / open eye | OpenAI | Auto-apply | pack | pack | 0 (pack) | |
| jira / gira / gyra / dura / jeera | Jira | Suggest | pack | pack | 0 (pack) | Apply when tickets, sprints or boards are in the sentence. |
| Lume / loom (lowercase, as a tool) | Loom | Suggest | pack | pack | 0 (pack) | Video messages. "Looming deadline" stays. |
| notion / motion | **Do not swap.** Notion and Motion are both real tools. | Watch | pack | pack | 0 (pack) | Record which one each speaker uses in the Notes cell. Never apply across them. |
| zap here / zappier / zap ear | Zapier | Suggest | pack | pack | 0 (pack) | |
| hub spot | HubSpot | Auto-apply | pack | pack | 0 (pack) | |
| air table | Airtable | Auto-apply | pack | pack | 0 (pack) | |
| get hub / git hub | GitHub | Auto-apply | pack | pack | 0 (pack) | |
| fig ma / sigma (in a design context) | Figma | Suggest | pack | pack | 0 (pack) | Sigma is also a real product. Apply only when designs, frames or prototypes are mentioned. |
| cursor (as a tool) | Cursor | Watch | pack | pack | 0 (pack) | Also an ordinary word. Watch until your calls show the pattern. |
| granola (as a tool) | Granola | Suggest | pack | pack | 0 (pack) | The note-taking app, not breakfast. |

## B. Code-switched phrases

None in this pack. See `packs/banglish/` for an example, or build your own with `docs/make-your-own-pack.md`.

| Raw | Resolves to | Confidence | Notes |
|---|---|---|---|

## C. Fillers & acknowledgements

| Raw | Resolves to | Confidence | Notes |
|---|---|---|---|
| um / uh / er / erm | _(drop)_ | Auto-apply | Drop in the readable transcript. Keep if the hesitation itself matters ("um... no, we didn't sign"). |
| you know / I mean / like (as filler) | _(drop)_ | Suggest | Only when it carries no meaning. "I mean the second invoice" is not filler. |
| mm-hm / mhm / uh-huh (alone on a turn) | "Mm-hm." | Auto-apply | Keep one, as a turn, so agreement stays visible. |
| yeah yeah yeah / yes yes yes | "Yeah." | Auto-apply | Collapse repeats. One sighting per call however often it happens. |
| sorry, go ahead / no, you go (crosstalk) | _(drop, or one line: [crosstalk])_ | Suggest | |
| a lone "OK" or "right" split across two turns by the ASR | merge into the speaker's next turn | Suggest | Common in tools that split turns on short pauses. |

## D. Names (verified against the people source, never invented)

Names are personal. This pack ships none. Add your people to `config/people.md`, and the skill will learn how their names get misheard.

| Raw | Person | People page | Confidence | Notes |
|---|---|---|---|---|

## E. Domain jargon

| Raw | Resolves to | Confidence | Notes |
|---|---|---|---|
| M.C.P / MCPs / em see pee | MCP (Model Context Protocol) | Suggest | |
| L.L.M / elem / LLMs | LLM | Auto-apply | |
| rag (in an AI context) | RAG (retrieval-augmented generation) | Suggest | "Rag" as a cloth stays. |
| S.O.P / sop | SOP | Auto-apply | |
| K.P.I / KPIs / kpi's | KPI / KPIs | Auto-apply | |
| A.S.R | ASR (automatic speech recognition) | Suggest | |
| P.O.C / proof of concept | POC | Suggest | |
