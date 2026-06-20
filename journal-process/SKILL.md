---
name: journal-process
description: Process voice journal recordings or pasted transcripts. Use when you say "process this recording", "clean up this journal", "journal process", or "/journal-process".
user-invocable: true
---

# Journal Process

## Purpose
Take voice journal recordings (from Granola, voice memos, or similar) and transform them into clean, structured entries for your weekly reflection file. Cleans up speech artifacts while preserving your voice, extracts natural structure, and appends to the appropriate day.

## When to Use
- "process this recording"
- "clean up this journal"
- "journal process"
- `/journal-process`
- When you paste a transcript or recording output

## Vault Paths
- **Vault root:** your notes vault (set this to your own path, e.g. an Obsidian/Logseq/plain-Markdown folder). Referred to below as `$VAULT_ROOT`.
- **Weekly reflections:** `reflections/weekly/[MM.DD.YY]-[MM.DD.YY].md`

---

## The Process

### Step 1: Get the Recording
Ask user to paste the transcript output.

> Paste your recording and let me know which day this is for.

If the day isn't specified, ask which day.

---

### Step 2: Clean the Transcript

**Remove:**
- Filler words (um, uh, like, you know, sort of, kind of, I mean, basically, literally, right?)
- False starts and repetitions
- Verbal stutters

**Fix:**
- Grammar and punctuation
- Run-on sentences (break into readable chunks)
- Obvious transcription errors

**Preserve:**
- Natural voice and phrasing
- Conversational asides and tangents (often valuable)
- The authentic feel of spoken reflection

**Do NOT:**
- Over-polish into formal writing
- Add content that wasn't said
- Remove personality or edge
- Sanitize opinions or frustrations

---

### Step 3: Infer Structure

Look at what was talked about and create natural sections. Don't force a template.

**If the content has clear topics:** Use headers like `## Morning Workout`, `## Work: The Project`, `## Evening Reflection`

**If it's stream-of-consciousness:** Keep as flowing paragraphs with minimal headers.

---

### Step 4: Extract Key Elements

At the end, add (only if relevant):

**Key Takeaways** (if there are clear insights):
```markdown
### Key Takeaways
- [Insight or realization]
```

**Action items** (if mentioned):
```markdown
### To Do
- [ ] [Thing mentioned as needing to be done]
```

Skip these sections entirely if nothing fits.

---

### Step 5: Show Draft for Approval

Before writing to the file, show the cleaned version:

> Here's the cleaned journal entry for [Day]:
>
> [formatted content]
>
> Ready to add this to your weekly reflection?

---

### Step 6: Append to Weekly Reflection

Once approved, find the current week's file in `reflections/weekly/` and add under the appropriate day header.

If no weekly file exists yet, create one using the standard format.

---

## Boundaries

**This skill DOES:**
- Clean up speech-to-text artifacts
- Structure content based on natural topics
- Preserve voice and opinions
- Append to existing weekly reflection files

**This skill does NOT:**
- Create new standalone files (appends to weekly)
- Add content that wasn't said
- Over-polish or formalize the writing
- Remove personality, edge, or frustration
- Process content without showing a draft first

## Voice
Clean but authentic. The goal is readability, not perfection. Reflections should sound like you, just without the "um"s.

## Chains To
- After processing: "Want me to run `/daily-process` to file any loose notes in your vault?"
- On Sunday: might chain to `/weekly-plan`
