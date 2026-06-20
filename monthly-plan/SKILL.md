---
name: monthly-plan
description: Monthly planning session — synthesis, content planning, and QoL booking. Use when you say "monthly plan", "plan the month", "monthly review", or "/monthly-plan". 2-hour session.
user-invocable: true
---

# Monthly Plan

## Purpose
The monthly sit-down that synthesizes the past month, plans content for the next, and books Quality of Life activities. 2-hour session covering reflection, content planning, and QoL booking.

**Core insight:** If it's not scheduled, it doesn't happen. This skill protects relationship, self-care, community, and creative work from being crowded out.

## When to Use
- 3rd or 4th Sunday of the month
- "monthly plan", "plan the month", "monthly review"
- `/monthly-plan`

## Vault Paths
- **Vault root:** your notes vault (set this to your own path, e.g. an Obsidian/Logseq/plain-Markdown folder). Referred to below as `$VAULT_ROOT`.
- **Weekly reflections:** `reflections/weekly/[MM.DD.YY]-[MM.DD.YY].md`
- **Quarterly plan:** `reflections/2026-plan/Q[X]-2026-plan.md`
- **Monthly plans:** `reflections/2026-plan/[month]-2026.md`
- **Editorial calendar:** `writing/editorial-calendar.md`
- **Ideas inbox:** `writing/ideas/inbox.md`
- **Drafts:** `writing/drafts/`

---

## The Process (2 hours total)

### Phase 1: Monthly Synthesis (30 min)

#### Step 1: Gather Weekly Reflections
Read all weekly reflection files from the current month (typically 4-5 files) from `reflections/weekly/`.

Ask: "What month are we reviewing and planning for?"

#### Step 2: Surface Patterns

Analyze the weekly reflections for:

**Recurring themes:** What topics came up multiple weeks?
**Energy patterns:** Which weeks felt energized vs. depleted?
**Open threads:** Unfinished thoughts or projects

Output a synthesis with themes, energy patterns, what got attention vs neglected, and open threads to carry forward.

#### Step 3: Reflection Prompts

> **Month Reflection Questions:**
> 1. What's one thing you're proud of from this month?
> 2. What pattern do you see in the energy fluctuations?
> 3. What got neglected that you want to prioritize next month?
> 4. Is there an open thread that's ready to become a project?

**PAUSE.** Wait for user to reflect before Phase 2.

---

### Phase 2: Content Planning (30 min)

#### Step 4: Review What's On Deck
Read `writing/editorial-calendar.md` and `writing/drafts/` folder.

Show drafts in progress and editorial calendar status for next month.

#### Step 5: Ideas Review
Read `writing/ideas/inbox.md` and show available ideas.

#### Step 6: Content Decisions
Prompt decisions about which drafts to finish, what topics fill gaps, and what the ONE priority piece is.

Update `writing/editorial-calendar.md` with assigned topics.

**PAUSE.** Confirm content plan before Phase 3.

---

### Phase 3: Quality of Life Booking (45 min)

#### Step 7: Date Night Booking
> "Let's schedule date nights for [month].
> - How many date nights? (Target: 2-4)
> - Any weeks blocked by travel/commitments?
> - What days typically work best?"

**If zero date nights:** Flag as a warning sign.

#### Step 8: Body Rituals
> "Body rituals. Standard is massage + facial each month.
> - Massage scheduled?
> - Facial scheduled?
> - Other body care?"

**If nothing scheduled:** Flag as warning.

#### Step 9: Friend/Community Time
> "Community time. Without scheduled social engagement, community collapses.
> - Standing dates with friends?
> - Hosting anything?
> - Group activities?"

**If 2+ weeks have no social plans:** Flag as warning.

#### Step 10: Cultural Activities
> "Any cultural activities to book? (theater, music, art, comedy, museums)"

---

### Phase 4: Create Month Plan File

Create `reflections/2026-plan/[month]-2026.md`:

```markdown
# [Month] 2026

**Planning date:** [Date]
**Status:** Active

---

## Month Synthesis

**Recurring themes from [previous month]:**
- [Theme 1]
- [Theme 2]

**Energy patterns:**
- [Notes]

**Key insight:** [One sentence from reflection]

**Carrying forward:**
- [Open thread 1]
- [Open thread 2]

---

## Content Plan

**Priority piece:** [The ONE that matters most]

**Drafts to finish:**
- [ ] [Draft 1]
- [ ] [Draft 2]

---

## Quality of Life Bookings

### Date Nights
| Date | Plan | Booked? |
|------|------|---------|
| | | [ ] |

### Body Rituals
- [ ] Massage: [Date]
- [ ] Facial: [Date]

### Community
| Date | Plan | Who |
|------|------|-----|
| | | |

### Cultural Activities
| Date | Activity | Booked? |
|------|----------|---------|
| | | [ ] |

---

## Warnings

[Any gaps or concerns flagged during planning]
```

---

### Final Summary

> **[Month] Planning Complete**
>
> **Content:** [X] articles planned
> **Date nights:** [X] scheduled
> **Body rituals:** [X] scheduled
> **Community:** [X] social plans
> **Warnings:** [Any gaps flagged]
>
> **Next:** Weekly rhythm kicks in. Run `/weekly-plan` each Sunday.

---

## Warning Sign Triggers

Flag explicitly:
- Zero date nights in a month
- 2+ weeks without scheduled social engagement
- No body rituals scheduled
- Editorial calendar gaps with no plan
- Same thing neglected 2+ months in a row

## Voice
Direct and protective. This session protects quality of life.

## Chains To
- After completing: "Weekly rhythm kicks in. Run `/weekly-plan` each Sunday."
- At end of month 3: "This is month 3 of the quarter. Next monthly includes quarterly planning — block 3 hours."
