---
name: requirements-builder
description: "Build structured user stories with acceptance criteria, edge cases, and scope boundaries for a feature. Use when the user says 'requirements', 'user stories', 'build requirements', 'what are the stories for', or after brainstorming when they say 'now build the stories' or 'pin down the requirements'. Also use when the user is about to implement something and hasn't defined clear acceptance criteria yet — this prevents mid-implementation drift by forcing edge cases and boundaries to be explicit before code is written."
---

# Requirements Builder

Turn a feature idea into structured user stories with acceptance criteria, edge cases, error handling, and explicit scope boundaries. Prevents mid-implementation drift by pinning down what "done" looks like before code is written.

## When to Use

- After brainstorming, to turn a design into implementable stories
- Before implementation, when you know what to build but haven't defined the edges
- When the user says "requirements", "user stories", or "what should this do exactly"

## The Process

### Step 0: Check for Context

Look for a recent design doc in `docs/plans/` related to the topic. If one exists, ask:

"I found [doc name]. Should I use this as context, or are we starting fresh?"

If warm-starting from a design doc, read it and pre-fill what you can. Only ask questions the doc doesn't answer.

### Step 1: Understanding (3-5 questions)

Ask these one at a time. Use multiple choice when possible. Skip any that are already answered by context.

1. **Who is the user?** There may be multiple user types. Identify each.
2. **What outcome do they want?** Not the feature — the result from their perspective.
3. **What triggers this?** What action or event kicks off the flow.
4. **What does "done" look like?** From the user's eyes, not yours.
5. **Hard constraints?** Tech limitations, time pressure, platform requirements.

Keep it conversational. If the answer to one question makes another obvious, skip it.

### Step 2: Checklist Sweep

This is the part that catches blind spots. Walk through each category one at a time, regardless of what was covered in Step 1. These categories exist because they're the things most often missed and discovered too late during implementation.

| Category | What to ask |
|----------|-------------|
| **Happy path** | "Walk me through the ideal flow step by step." |
| **Empty/null states** | "What happens when there's no data yet? First-time user experience?" |
| **Error states** | "What can fail? What does the user see when it does?" |
| **Boundaries** | "What is explicitly NOT in scope? What should this never do?" |
| **Edge cases** | "What's the weird input? The power user abuse case? The off-by-one?" |
| **Data** | "What's created, read, updated, or deleted? Any state changes?" |

If a category genuinely doesn't apply, the user says "skip" and you move on. But always ask — the point is to surface things the user hasn't thought about, not to confirm what they already know.

### Step 3: Generate the Requirements Doc

After the interview, write the requirements document to `docs/plans/YYYY-MM-DD-<topic>-requirements.md`.

Use this structure:

```markdown
# Requirements: <Feature Name>

## Context
One paragraph — what this is and why it matters.
Link to design doc if one exists.

## Users
Who this is for (from Step 1).

## User Stories

### Story 1: <Short name>
**As a** [user type], **I want** [action] **so that** [outcome].

**Acceptance criteria:**
- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

**Edge cases:**
- What happens when [unusual input/state]
- What happens when [boundary condition]

**Error handling:**
- When [X fails], user sees [Y]

### Story 2: <Short name>
...

## NOT In Scope
- Thing 1 — why it's deferred
- Thing 2 — why it's deferred

## Open Questions
Anything unresolved from the interview.
```

Guidelines for writing good stories:
- Each story should be independently implementable where possible
- Acceptance criteria should be checkboxes — binary pass/fail, no ambiguity
- Edge cases come from the Checklist Sweep — don't invent ones that weren't discussed
- "NOT In Scope" is just as important as the stories. Be explicit about what you're choosing not to build and why. This is the primary defense against scope creep.

### Step 4: Load into Tasks

After writing the doc, ask:

"Ready to load these into tasks for implementation?"

If yes, create a TodoWrite entry for each user story. Use the story name as the task content and include the acceptance criteria in the description. This way the stories are in your face during implementation — you can't drift if the checklist is staring at you.

## Key Principles

- **One question at a time.** Don't overwhelm. Let the user think.
- **Multiple choice when possible.** Easier to answer, faster to converge.
- **The checklist always runs.** That's the whole point — it catches what you'd otherwise miss. Skipping categories is fine; skipping the sweep is not.
- **Stories are contracts.** If it's not in the acceptance criteria, it's not required. If it's in "NOT In Scope", it's not allowed. This clarity is what prevents drift.
- **Warm start saves time.** If brainstorming already happened, don't re-ask answered questions. Read the design doc and focus on gaps.
