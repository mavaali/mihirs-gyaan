---
name: quarterly-plan
description: Quarterly planning session — deep review and focus areas for next 12 weeks. Use when you say "quarterly plan", "plan the quarter", or "/quarterly-plan". 3-hour session.
user-invocable: true
---

# Quarterly Plan

## Purpose
The quarterly sit-down that reviews the past 12 weeks, surfaces patterns from monthly syntheses, and sets 2-3 focus areas for the next quarter. 3-hour session with deep reflection and intentional planning.

**Core insight:** The quarterly is where pattern recognition happens at scale. Monthly syntheses roll up, and you step back to see the bigger picture.

## When to Use
- Week 11 of each quarter (or start of a new quarter)
- "quarterly plan", "plan the quarter", "quarterly review"
- `/quarterly-plan`

## Vault Paths
- **Vault root:** your notes vault (set this to your own path, e.g. an Obsidian/Logseq/plain-Markdown folder). Referred to below as `$VAULT_ROOT`.
- **Monthly plans:** `reflections/2026-plan/[month]-2026.md`
- **Quarterly plans:** `reflections/2026-plan/Q[X]-2026-plan.md`
- **Annual plan:** `reflections/2026-plan/2026-plan.md`
- **Weekly reflections:** `reflections/weekly/`

---

## The Process (3 hours)

### Phase 1: Review the Past Quarter (60 min)

#### Step 1: Gather Monthly Syntheses
Read the 3 monthly plan files from the quarter being reviewed.

Ask: "Which quarter are we reviewing? (e.g., Q1 2026 = January-March)"

#### Step 2: Roll Up Patterns

Across all 3 months, identify:

**Themes that persisted all quarter:**
- What kept coming up month after month?

**Energy arc:**
- How did energy shift across the quarter?
- Which month felt best? Which felt hardest?

**What got consistent attention:**
- Projects, domains, relationships that thrived

**What got consistently neglected:**
- What fell off despite intentions?

**QoL compliance:**
- Date nights per month
- Body rituals per month
- Community engagement per month
- Cultural activities per month

#### Step 3: Focus Area Review

Read the previous quarter's plan and evaluate each focus area:

> **Q[X] Focus Area Review:**
>
> **Focus 1: [Name]**
> - What happened: [Evidence from monthly syntheses]
> - Outcome: [Met / Partially met / Not met]
>
> **Focus 2: [Name]**
> - What happened: [Evidence]
> - Outcome: [Met / Partially met / Not met]

#### Step 4: Deep Reflection

> **Quarterly Reflection Questions (take 15-20 min):**
> 1. What's the story of this quarter in one paragraph?
> 2. What surprised you?
> 3. What would you tell yourself 12 weeks ago?
> 4. What structure or habit served you best?
> 5. What structure or habit needs to change?
> 6. Where are you relative to your annual direction?

**PAUSE.** Wait for user to reflect before Phase 2.

---

### Phase 2: Set Next Quarter's Focus (45 min)

#### Step 5: Annual Plan Check

Read `reflections/2026-plan/2026-plan.md` (if it exists).

> "Here's your annual direction. How does the next quarter serve it?"

#### Step 6: Choose Focus Areas

> "For Q[X+1], choose 2-3 focus areas. These should be:
> - Specific enough to measure
> - Broad enough to sustain 12 weeks
> - Connected to what matters (not just what's urgent)
>
> Based on the review, I'd suggest considering:
> - [Suggestion based on neglected areas]
> - [Suggestion based on energy patterns]
> - [Suggestion based on open threads]"

**PAUSE.** User decides their focus areas.

#### Step 7: Structure Transitions

> "Any structural changes needed?
> - Routines to add/remove?
> - Tools or systems to change?
> - Commitments to adjust?"

---

### Phase 3: Create Quarter Plan (30 min)

#### Step 8: Create Quarterly Plan File

Create `reflections/2026-plan/Q[X]-2026-plan.md`:

```markdown
# Q[X] 2026

**Planning date:** [Date]
**Status:** Active

---

## Quarter Review: Q[X-1]

**Story of the quarter:**
[One paragraph summary]

**Focus area outcomes:**
- [Focus 1]: [Outcome]
- [Focus 2]: [Outcome]

**QoL compliance:**
- Date nights: [X/month average]
- Body rituals: [X/month average]
- Community: [X/month average]

**Key insight:** [One sentence]

---

## Q[X] Focus Areas

### Focus 1: [Name]
**Why:** [Connection to annual direction or pattern]
**What success looks like:** [Measurable or observable]
**Monthly check:** [What to look for]

### Focus 2: [Name]
**Why:** [Connection]
**What success looks like:** [Measurable]
**Monthly check:** [What to look for]

### Focus 3: [Name] (optional)
**Why:** [Connection]
**What success looks like:** [Measurable]
**Monthly check:** [What to look for]

---

## Structure Changes

- [Routine/system changes for this quarter]

---

## Month 1 Priorities

[Seed the first monthly plan with initial priorities]
```

---

### Final Summary

> **Q[X] Planning Complete**
>
> **Review:** Q[X-1] summarized with [X] focus areas evaluated
> **New focus areas:** [List them]
> **Structure changes:** [List them]
>
> **Next:** Run `/monthly-plan` to plan the first month of the quarter.

---

## Boundaries

**This skill DOES:**
- Roll up monthly syntheses into quarterly patterns
- Evaluate previous focus areas against evidence
- Guide selection of new focus areas
- Create the quarterly plan file

**This skill does NOT:**
- Access external trackers (user reports that data)
- Make decisions about focus areas (guides, user decides)
- Plan specific months (that's `/monthly-plan`)

## Voice
Reflective and honest. This is the big-picture session. Don't rush it.

## Chains To
- After completing: "Run `/monthly-plan` to plan the first month."
