# Make your own pack

A pack is a set of glossary rows other people can merge into their own glossary. Make one for your languages, your industry, or your team's tools.

## 1. Start from evidence, not from a list

The best pack rows come out of a glossary that has been running on real calls for a few weeks. Open your `glossary/glossary.md` and look for rows at Auto-apply. Those are patterns three or more separate calls agreed on.

Rows you invented from imagination ("people probably mishear X as Y") belong at Watch, if at all.

## 2. Strip everything personal

Before a row leaves your machine:

- Remove every real name. Category D in a public pack is fictional examples only, clearly marked.
- Remove client, company and project names that are not public products.
- Remove numbers, dates and quotes that came from a real call.
- Rewrite the Notes cell so it explains the *context* that makes the row safe, using a made-up sentence.

A good Notes cell: `Apply when tickets, sprints or boards are in the sentence.`
A bad Notes cell: a quote from last Tuesday's call with a client.

## 3. Use the same five categories and schemas

| Category | Columns |
|---|---|
| A. Proper nouns | Raw \| Resolves to \| Confidence \| First seen \| Last seen \| Sightings \| Notes |
| B. Code-switched phrases | Raw \| Resolves to \| Confidence \| Notes |
| C. Fillers & acknowledgements | Raw \| Resolves to \| Confidence \| Notes |
| D. Names | Raw \| Person \| People page \| Confidence \| Notes |
| E. Domain jargon | Raw \| Resolves to \| Confidence \| Notes |

In a pack, set First seen and Last seen to `pack` and Sightings to `0 (pack)`, so the importer's own count starts clean.

## 4. Choose tiers honestly

| Ship at | When |
|---|---|
| Auto-apply | You saw it in many distinct calls, and the replacement is safe in almost every sentence ("chat GBT" → ChatGPT) |
| Suggest | The meaning is clear but context matters ("money" mid-sentence → *mane*, "I mean") |
| Watch | Both sides are real words or real products ("notion" / "motion"), or you have seen it only once |

Some of the most useful rows are refusals: "do not swap these two". Put them at Watch with the reason in Notes.

## 5. Write rules as rules

Not every row is a word swap. The Banglish honorific row says "split *bhai* off the name". A filler row says "drop it, unless the hesitation matters". Write the rule in the Resolves to cell in plain words, and the exception in Notes.

## 6. Package it

```
packs/<your-pack>/
  README.md   who it is for, what is in it, how to install, why each Auto-apply row earned it
  pack.md     the five category tables
```

Look at `packs/banglish/` for a worked example.

## 7. Share it

Open a pull request against this repo, or publish the folder anywhere. Run your own deny-list scan before you share: search the pack for every name, company and email address from your real glossary. If one shows up, the pack is not ready.
