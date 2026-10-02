# learning-glossary

**Clean messy meeting transcripts with a glossary that learns your words, and refuses to trust a single sighting.**

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-v0.1.0-green.svg)](CHANGELOG.md)
![Works with](https://img.shields.io/badge/works%20with-Claude%20Code%20%C2%B7%20Claude%20Projects%20%C2%B7%20ChatGPT%20%C2%B7%20Cursor%20%C2%B7%20Codex-informational.svg)

## The story

Half my calls switch between Bangla and English mid-sentence. A colleague says *achha* and the transcript says "4". Someone mentions Monday.com and I read "muddy dot com". I ask about Claude Code and get "cloth code". A respected colleague addressed as *Tareq bhai* turns into a man called "Tareq By".

For months I fixed the same words by hand, every call. An AI could fix them for me, but only if it remembered last week's fixes. And if it remembered them too eagerly, one bad guess would rewrite every transcript after it.

So I built a glossary that learns my words but refuses to trust one sighting. A new word gets watched first. Then it gets applied with a flag I can check. Only when three separate calls agree does it get applied on sight. Now "cloth code" fixes itself, and anything new still shows up in a short table at the bottom of the note, waiting for me to confirm.

Most AI setups forget. This one compounds.

## 60-second quickstart

**Claude Code**

```bash
git clone https://github.com/itstauf/learning-glossary
cd learning-glossary
cp glossary/glossary.template.md glossary/glossary.md   # or let the skill do it on first run
```

Open Claude Code in the folder, paste a transcript and say **"clean this transcript"**. You get:

- a cleaned note in `meetings/`, with summary, decisions, action items and a *Contradictions & things to verify* table;
- a glossary that now knows a little more, with a dated entry at the top of its growth log saying exactly what changed.

Optional: merge a starter pack from `packs/` (Banglish or English) so your glossary does not start empty.

Want to see it before you try it? Read `examples/walkthrough.md`: one word climbing from Watch to Auto-apply across three synthetic calls.

## How it works

Every pattern in the glossary sits on a three-rung ladder. It climbs only on evidence, and evidence means **distinct transcripts**. Twenty repeats in one call still count as one.

```
   new word, meaning unclear          new word, meaning clear
             │                                  │
             ▼                                  │
     ┌──────────────┐  a later call makes       │
     │    WATCH     │  the meaning clear        │
     │ record only, │ ──────────────────┐       │
     │ never apply  │                   ▼       ▼
     └──────────────┘            ┌──────────────────┐
                                 │     SUGGEST      │
                                 │ apply, and flag  │
                                 │ it in the note   │
                                 └────────┬─────────┘
                                          │ 3rd distinct transcript
                                          ▼
                                 ┌──────────────────┐
                                 │    AUTO-APPLY    │
                                 │ replace on sight,│
                                 │ still checked    │
                                 │ against context  │
                                 └──────────────────┘
          only you move a row down, or delete it
```

Five guards keep it from poisoning itself:

1. New entries never go straight to Auto-apply.
2. Auto-apply is still context-checked. If the swap makes nonsense, it is flagged, not applied.
3. Names are verified against a people source (`config/people.md`). No invented people.
4. You co-own the file. Promote, demote or delete any row by hand.
5. Nothing is silent. Every change goes into an append-only growth log, newest on top.

One more rule holds it together: **only the `clean-transcript` skill writes the glossary.** Capture tools hand it transcripts and step back. That way there is one place deciding what your words mean.

Under the hood the skill runs seven phases: intake, load the glossary (in pages, because it grows), speaker segmentation, reconstruct by tier, assemble the note, update the glossary and growth log, report.

Deeper reading: `docs/how-the-ladder-works.md`, `docs/the-five-guards.md`, `docs/single-writer.md`.

A markdown knowledge base maintained by an LLM is a common idea now, and I credit Andrej Karpathy's LLM wiki pattern for it. What this series adds is the part most setups skip: how the system decides what is true, how it polices its own output, and how it grows its own tools. This repo is the first of those: a rule for when a guess becomes a fact.

## Use it your way

### Claude Code

The skill is already in place at `.claude/skills/clean-transcript/SKILL.md`. To use it in another repo, copy that folder plus `glossary/glossary.template.md` and `config/`. Triggers: "clean this transcript", "clean this call", "clean the inbox".

Drop exported files (`.txt`, `.vtt`, `.srt`) in `transcripts/inbox/` and say "clean the inbox". See `adapters/paste-or-upload.md`.

Use Granola? `adapters/granola/` adds a folder-scoped, manual-trigger capture: `/granola-tick` pulls new calls from one Granola folder and hands each to `clean-transcript`. It checks it is talking to the account you expect before it pulls anything. Otter, Fireflies, Zoom or Teams: export a `.vtt` and see `adapters/others.md`.

### Claude.ai Projects or ChatGPT Projects

Paste `prompts/project-instructions.md` into the project instructions. Upload your `glossary.md` (start from the template) and `people.md` as project knowledge. Paste a transcript, get back the cleaned note and a glossary diff. Paste the diff into your glossary and re-upload it before the next call. The model never edits your file; you do.

### Cursor, Codex, or any agent that reads AGENTS.md

`AGENTS.md` points the agent at the same skill file and lists the hard rules. Nothing in the procedure is specific to one vendor.

### No agent

Read it as a method. `docs/how-the-ladder-works.md` and `examples/` are enough to run the ladder by hand in a spreadsheet: one row per mishearing, a column for distinct calls, a rule that nothing applies silently until three calls agree.

### Running it with a team

- **One glossary per team, one writer.** The skill writes; people correct. Corrections in chat ("that was a person, not the tool") are logged as "(user correction)".
- **Protect the file.** Put the glossary and people source behind review with a CODEOWNERS rule, for example `glossary/ @your-ops-lead` and `config/people.md @your-ops-lead`, so promotions and new names get a second pair of eyes.
- **Review gate.** Ask whoever owns the call to skim the Contradictions table before the note is shared. It is short on purpose.
- **Keep raw transcripts out of git** unless everyone on the call agreed. `.gitignore` already excludes `transcripts/inbox/` and staged Granola folders.

## What it will not do (honest limits)

- **It is a procedure an agent runs, not a model.** There is no fine-tuning and no code that runs on its own. Quality depends on the agent and model you run it with. A weaker model will miss context checks a stronger one catches.
- **It does not transcribe.** It cleans what your recording tool produced. Garbage in still limits what comes out.
- **Large glossaries need paged reads.** After a few months mine passed a thousand lines. The skill reads it in pages and edits only the slice it has read. That works, but it costs time on every run.
- **There is no retrieval index.** Lookup is the agent reading tables. Past a few thousand rows you would want search, and this repo does not ship it.
- **Names need a people source.** Without `config/people.md` (or your own equivalent), the skill will flag names, not learn them. That is deliberate.
- **Three agreeing calls can still be wrong.** If the same mishearing is resolved the same wrong way three times and nobody reads the flags, a wrong row reaches Auto-apply. The guards slow mistakes down and make them visible. Reading the table is still your job.
- **Wrong-script output is out of reach.** Some tools render Bangla in another script entirely. The glossary marks that as "leave verbatim" rather than guessing.

## FAQ

**Why count distinct transcripts instead of occurrences?**
One person's habit in one meeting proves very little. A long call where someone says "you no track" twenty times would otherwise promote a guess to Auto-apply in a single sitting. Three separate calls, often with different people and microphones, are real evidence.

**Why three?**
It is the smallest number that rules out one bad recording and one person's accent on one day, and small enough that a genuine pattern climbs within a couple of weeks of normal calls. You can change `promote_at` in `config/clean-transcript.json`. Keep it above one.

**Pack rows arrive at Auto-apply. Doesn't that break guard 1?**
Guard 1 limits the skill: it may not promote anything on thin evidence. A pack is evidence collected elsewhere and imported by you, on purpose (guard 4). If you would rather your own calls earn every row, set the pack rows to Suggest before merging. Three calls later the ladder will have caught up.

**Does it work for languages other than Bangla?**
Yes. Nothing in the skill is Bangla-specific. Category B holds whatever code-switching your calls have: Hindi-English, Spanish-English, Arabic-French. Start with the English pack and build your own with `docs/make-your-own-pack.md`.

**What happens when it gets something wrong?**
Tell it in chat, or edit the row yourself. Demote it, rewrite it or delete it. Add a growth-log line so you remember why. The skill never demotes on its own and never silently rewrites history.

**Can I use it without Granola or any connector?**
Yes, and that is the default. Paste a transcript or drop a file in `transcripts/inbox/`. Adapters are optional.

## Credits

- **Log every change, regenerated rule digest:** the legibility doctrine from Tom, YC Root Access, video 01 ("the self-improving company"). The growth log is that idea applied to a glossary.
- **Markdown knowledge base maintained by an LLM:** Andrej Karpathy's LLM wiki pattern.
- **Thin harness, skills as markdown:** Answer This, YC Root Access, video 04.
- Built by Taufiq uz Zaman from a glossary that has been cleaning my own calls since mid-2026, including one paid engagement, under NDA. Every example here is synthetic.

## Part of The Compounding Brain

> I hired the best person in the world for my job. On day one they knew nothing about my business, and by tomorrow they had forgotten today. So I stopped looking for a smarter AI and built it a memory that earns what it believes.

This repo is **the glossary that learns my words**. Read the chapter: [The glossary that learns my words](https://itstauf.com/resources/second-brain/glossary?utm_source=github&utm_medium=readme&utm_campaign=compounding-brain&utm_content=learning-glossary). The capture adapters belong to [The night shift](https://itstauf.com/resources/second-brain/night-shift?utm_source=github&utm_medium=readme&utm_campaign=compounding-brain&utm_content=learning-glossary).

| Repo | What it does |
|---|---|
| [brain-starter](https://github.com/itstauf/brain-starter) | The house: plain files, three memories, load order, skills that write skills |
| **learning-glossary** (you are here) | Learns your words: Watch, Suggest, Auto-apply on transcripts |
| [evidence-ladder](https://github.com/itstauf/evidence-ladder) | Same ladder, different job: learns patterns, not words |
| [the-critic](https://github.com/itstauf/the-critic) | Checks output with an adversarial reviewer |
| [brain-map](https://github.com/itstauf/brain-map) | Checks structure with a link graph and ripple queries |

Each repo stands alone. None requires another.

- The whole guide: [The Compounding Brain](https://itstauf.com/resources/second-brain?utm_source=github&utm_medium=readme&utm_campaign=compounding-brain&utm_content=learning-glossary)
- What to build first: [Build order](https://itstauf.com/resources/second-brain/build?utm_source=github&utm_medium=readme&utm_campaign=compounding-brain&utm_content=learning-glossary)
- Building your own? Join [Brain Builders](https://itstauf.com/resources/second-brain?utm_source=github&utm_medium=readme&utm_campaign=compounding-brain&utm_content=learning-glossary#brain-builders)

MIT licensed. Copyright 2026 Taufiq uz Zaman.
