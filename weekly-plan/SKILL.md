---
name: weekly-plan
description: Sunday weekly planning session. Use when you say "weekly plan", "plan the week", "Sunday planning", or "/weekly-plan". 30-45 minute session.
user-invocable: true
---

# Weekly Plan

## Purpose
The Sunday pulse check. Surface patterns from the past week, create next week's reflection file with priorities loaded from quarterly/monthly plans.

## When to Use
- Every Sunday
- "weekly plan", "plan the week", "Sunday planning"
- `/weekly-plan`

## Vault Paths
- **Vault root:** your notes vault (set this to your own path, e.g. an Obsidian/Logseq/plain-Markdown folder). Referred to below as `$VAULT_ROOT`.
- **Weekly reflections:** `reflections/weekly/[MM.DD.YY]-[MM.DD.YY].md`
- **Quarterly plan:** `reflections/2026-plan/Q[X]-2026-plan.md`
- **Monthly plan:** `reflections/2026-plan/[month]-2026.md`
- **Weekly template:** `templates/weekly-reflection.md`

---

## The Process

### Step 1: Find This Week's Reflection
Read the current week's reflection file from `reflections/weekly/`.

Weekly files are named `[MM.DD.YY]-[MM.DD.YY].md` (Monday-Sunday range).

If no file exists for this week, note that and proceed — the weekly may have been sparse.

---

### Step 2: Surface the Week

Review the week's reflection file and present:

> **Week in Review: [date range]**
>
> **What happened:**
> - [Key events, activities, observations from each day]
>
> **Themes:**
> - [Recurring topics or patterns across the week]
>
> **Energy pattern:**
> - [High/low days and what drove them]
>
> **Open threads:**
> - [Things mentioned but not resolved]

---

### Step 3: Check Against Monthly/Quarterly

Read the current quarterly and monthly plans.

> **Alignment Check:**
>
> **Quarterly focus areas:**
> - [Focus 1]: [Did this week serve it? How?]
> - [Focus 2]: [Did this week serve it? How?]
>
> **Monthly priorities:**
> - [Priority 1]: [Progress this week]
> - [Priority 2]: [Progress this week]
>
> **QoL bookings this week:**
> - [What was scheduled? Did it happen?]

---

### Step 4: Reflection Prompts

> **Quick Reflection (5 min):**
> 1. What's one thing you're carrying into next week — unfinished or weighing on you?
> 2. What worked this week that you want to repeat?
> 3. What's one thing you'd do differently?

**PAUSE.** Wait for user to reflect before creating next week's file.

---

### Step 5: Create Next Week's File

Calculate next week's date range (Monday-Sunday) and create:
`reflections/weekly/[MM.DD.YY]-[MM.DD.YY].md`

If a template exists at `templates/weekly-reflection.md`, use it. Otherwise use this format:

```markdown
# [MM.DD.YY] - [MM.DD.YY]

**Quarterly focus:** [Current quarter's focus areas]
**Monthly priority:** [Current month's key priority]
**Carrying forward:** [From step 4 reflection]

---

## Monday [MM.DD.YY]

## Tuesday [MM.DD.YY]

## Wednesday [MM.DD.YY]

## Thursday [MM.DD.YY]

## Friday [MM.DD.YY]

## Saturday [MM.DD.YY]

## Sunday [MM.DD.YY]

---

## Week Summary
<!-- Fill at end of week -->
```

---

### Step 6: Summary

> **Weekly Planning Complete**
>
> **Last week:** [1-sentence summary]
> **Carrying forward:** [Key thread]
> **Next week's file:** Created at `reflections/weekly/[range].md`
>
> **Reminder:** Run `/daily-process` if you have unfiled notes in the vault root.

---

## Boundaries

**This skill DOES:**
- Review the past week's reflection
- Check alignment with quarterly/monthly plans
- Create next week's reflection file with context loaded
- Surface patterns conversationally

**This skill does NOT:**
- Write reflections for you (you fill in daily entries)
- Make decisions about priorities (shows data, you decide)
- Modify monthly/quarterly plans

## Voice
Brief and observational. Like a coach checking in on Sunday evening. Don't over-analyze — surface the patterns and let the user sit with them.

## Chains To
- After completing: "Want me to run `/daily-process` to file any loose notes?"
- At end of month: "This is the last week of the month. Time for `/monthly-plan` next Sunday."
