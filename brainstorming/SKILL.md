---
name: brainstorming
description: "Use before any creative work - creating features, building components, adding functionality, or modifying behavior. Challenges the premise, explores alternatives, then designs the solution."
---

# Brainstorming Ideas Into Designs

## Overview

Turn ideas into fully formed designs through collaborative dialogue that challenges assumptions before committing to solutions.

Start by understanding the current project context. Before designing anything, challenge the premise. Then ask questions one at a time to refine the idea. Present the design in small sections (200-300 words), checking after each section.

## The Process

### Step 0: Premise Challenge (before anything else)

Before accepting the request at face value:

1. **Is this the right problem?** Could a different framing yield a simpler solution?
2. **What's the actual user outcome?** Strip away implementation language. What does the user actually get?
3. **Is this the most direct path?** Name at least one alternative approach that solves the same outcome differently.
4. **What does this displace?** Every new thing pushes something else aside. Name it.
5. **What exists already?** Map every sub-problem to existing code, libraries, or prior art. Explain why building new is better than reusing, if applicable.

Present the premise challenge concisely. If the premise holds, say so and move on. If it doesn't, say so directly and propose the reframe.

### Step 1: Understanding the idea

- Check out the current project state first (files, docs, recent commits)
- Ask questions one at a time to refine the idea
- Prefer multiple choice questions when possible, but open-ended is fine too
- Only one question per message
- Focus on: purpose, constraints, success criteria, who benefits and how

### Step 2: Scope decision

Before exploring approaches, make an explicit scope call. Present three options:

- **Expand**: What's 10x more ambitious for 2x effort? What's the version that would delight?
- **Hold**: Bulletproof this exact scope. Catch every failure mode, test every edge case.
- **Reduce**: Surgical cut to essentials. Minimum viable version achieving core outcome.

Recommend one with reasoning. Get agreement before proceeding.

### Step 3: Exploring approaches

- Propose 2-3 different approaches with trade-offs
- For each approach, name: what it solves well, what it handles poorly, what it assumes
- Lead with your recommended option and explain why
- Include one approach from outside the obvious domain (cross-domain pattern)

### Step 4: Presenting the design

Once you understand what you're building, present the design:
- Break it into sections of 200-300 words
- Ask after each section whether it looks right so far
- Cover: architecture, components, data flow, error handling, testing
- For every data flow, trace four paths: happy, nil/empty, error, upstream failure
- Be ready to go back and clarify if something doesn't make sense

### Step 5: Failure mode check

Before finalizing, explicitly enumerate:
- **What breaks if this succeeds wildly?** (scale, load, edge cases at volume)
- **What breaks if this fails?** (rollback, user impact, data state)
- **What's the 6-month consequence?** Does this solve today's problem without creating next quarter's nightmare?

## After the Design

**Documentation:**
- Write the validated design to `docs/plans/YYYY-MM-DD-<topic>-design.md`
- Include a "NOT in scope" section with deferred work and one-line rationale for each
- Include a "What already exists" section listing code/libraries that solve sub-problems
- Use elements-of-style:writing-clearly-and-concisely skill if available
- Commit the design document to git

**Implementation (if continuing):**
- Ask: "Ready to set up for implementation?"
- Set up an isolated workspace (a fresh branch or git worktree). If your host has a dedicated skill for this (e.g. `superpowers:using-git-worktrees`), use it.
- Write a detailed implementation plan before coding. If your host has a planning skill (e.g. `superpowers:writing-plans`), use it; otherwise write the plan to a Markdown file and work through it step by step.

## Key Principles

- **Challenge the premise first** - Don't accept the request at face value. Ask "should we?" before "how should we?"
- **One question at a time** - Don't overwhelm with multiple questions
- **Multiple choice preferred** - Easier to answer than open-ended when possible
- **YAGNI ruthlessly** - Remove unnecessary features from all designs
- **Explore alternatives** - Always propose 2-3 approaches before settling
- **Cross-domain pattern** - Before concluding, identify one analogous pattern from outside the current domain
- **Name the displacement** - Before accepting any new commitment, name what it displaces
- **Trace all paths** - Happy path is not enough. Trace nil, empty, error, and upstream failure
- **Incremental validation** - Present design in sections, validate each
- **Be direct** - If the idea is bad, say so. If the scope is wrong, say so. Product thinking requires honesty, not facilitation.

---

*Adapted from the `brainstorming` skill in [obra/superpowers](https://github.com/obra/superpowers) (MIT © Jesse Vincent). The premise-challenge, scope-decision, and failure-mode steps were added here. See [CREDITS](../CREDITS.md).*
