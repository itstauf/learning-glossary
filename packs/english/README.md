# English pack

Common mishearings from English-language calls about software, AI tools and operations, plus filler handling.

## What is in it

| Category | What | Examples |
|---|---|---|
| A. Proper nouns | 14 tool names | "cloud code" → Claude Code, "Lume" → Loom, "gira" → Jira, "zap here" → Zapier |
| C. Fillers & acknowledgements | 6 rules | drop "um" / "uh", collapse "yeah yeah yeah", keep one "Mm-hm." |
| E. Domain jargon | 7 acronyms | "M.C.P" → MCP, "L.L.M" → LLM, "rag" → RAG (in an AI context) |

Categories B (code-switched phrases) and D (names) are empty on purpose. Code-switching depends on your languages, and names depend on your people.

## The rows that refuse to swap

Some rows exist to stop a mistake, not to fix one. "notion" and "motion" are both real products, so the row sits at Watch with the instruction "do not swap". Its job is to remind the agent that a confident-looking correction here would be a guess. "cursor" and "sigma" get the same caution.

If your team only ever uses one of the pair, raise the row to Suggest yourself and write why in the Notes cell. That is guard 4: you co-own the file.

## How to install

1. Make sure `glossary/glossary.md` exists (copy `glossary/glossary.template.md`, or run `clean-transcript` once).
2. Copy the rows you want from `pack.md` into the matching tables in your glossary.
3. Add one growth-log entry at the top of the log, for example:
   `### 2026-10-03 (user: merged English pack, Categories A, C, E)`.

Packs can be combined. Merge the English pack and the Banglish pack and keep whichever row is stricter where they overlap (for Claude / Claude Code, both packs agree).
