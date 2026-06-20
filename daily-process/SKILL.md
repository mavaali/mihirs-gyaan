---
name: daily-process
description: Process unfiled notes and surface daily observations. Use at end of day or when you say "process the day", "daily processing", "organize my notes", or "/daily-process".
user-invocable: true
---

# Daily Process

## Purpose
End-of-day note hygiene and pattern surfacing. Finds notes that haven't been filed, adds proper metadata, moves them to the right folder, and surfaces observations about what's on your mind.

## When to Use
- "process the day"
- "daily processing"
- "organize my notes"
- `/daily-process`
- End of day when you want to close loops

## Vault Paths
- **Vault root:** your notes vault (set this to your own path, e.g. an Obsidian/Logseq/plain-Markdown folder). Referred to below as `$VAULT_ROOT`.
- **Fleeting notes:** `fleeting/`
- **Literature notes:** `literature/`
- **Ideas:** `ideas/`

---

## The Process

### Step 1: Scan for Unfiled Notes
Find all `.md` files in the vault root (not in organized folders).

> "Let me scan your vault for unfiled notes..."

**If no unfiled notes:** Skip to Step 5 and reflect on the day without file processing.

---

### Step 2: Classify Each Note

For each unfiled note, read the content and determine:

#### Folder Assignment
- **Fleeting**: Raw thoughts, quick captures, fragments, questions without answers, brain dumps
- **Literature**: References external content — books, articles, podcasts, videos, quotes from others
- **Ideas**: Developed thinking, concepts being explored, synthesis of multiple ideas

#### Tag Inference
Scan content for domain signals and assign relevant tags.

#### State Assignment
- `seed` — Very rough, just a question or fragment
- `sprout` — Has some substance but undeveloped
- `leafing` — Has structure, emerging ideas, being actively developed

---

### Step 3: Add YAML Front Matter

For each note, add or update front matter:

```yaml
---
title: [filename without extension]
date_created: [today's date YYYY-MM-DD]
tags:
  - [type tag: fleeting/literature/idea]
  - [domain tag(s) inferred from content]
state: [seed/sprout/leafing]
publish: false
---
```

**If front matter exists:** Preserve existing values, only add missing fields.

---

### Step 4: Move to Correct Folder

Move each note to its determined folder:
- Fleeting notes -> `fleeting/`
- Literature notes -> `literature/`
- Idea notes -> `ideas/`

---

### Step 5: Daily Reflection

After processing (or if no notes to process), share observations in chat:

> **Daily Processing Complete**
>
> **Notes processed:** [count]
> - [note title] -> [folder] (tags: [tags])
>
> **Patterns I notice:**
> [What themes emerged across today's notes?]
>
> **Observation:**
> [One reflection on what these notes suggest about where your attention is]

This reflection is conversational and ephemeral — it does NOT get saved to a file.

---

## Boundaries

**This skill DOES:**
- Process notes in the vault root only
- Add missing front matter
- Move notes to appropriate folders
- Surface patterns conversationally

**This skill does NOT:**
- Touch notes already in organized folders (bookmarks, learnings, snippets, people, reflections)
- Create permanent reflection files
- Modify existing front matter values (only adds missing fields)
- Process non-markdown files
- Reorganize the folder structure

## Voice
Direct, observational. Like a thoughtful assistant helping you close out the day. No excessive commentary — just what was done and what patterns emerged.

## Chains To
- This skill should be **chained from other skills** to ensure it gets used:
  - After `/weekly-plan`: "Did you run `/daily-process` this week?"
  - After `/journal-process`: "Want me to file any loose notes?"

## The Chaining Lesson

**Important:** Skills for personal productivity need hooks. Make sure to chain this to something you already do regularly. Without an external trigger, it gets forgotten.
