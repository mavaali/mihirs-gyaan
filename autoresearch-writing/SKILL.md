---
name: autoresearch-writing
description: "Iteratively improve a piece of writing with a Karpathy-autoresearch-style loop: score it against a rubric, make ONE change per experiment, keep or revert based on the score delta, repeat until it stops improving. Works for any writing — essays, blog posts, emails, docs, reports, talks — with a pluggable rubric calibrated to your voice and genre. Use when asked to 'iterate this draft', 'run the loop on this', 'tighten this piece', or '/autoresearch-writing <path>'."
user-invocable: true
---

# autoresearch-writing

A disciplined editing loop. You do NOT freestyle edits. You score the piece against an
explicit rubric, change exactly one thing to fix the lowest dimension, then keep the change
only if the score went up and no anti-pattern crept in. Otherwise you revert. Repeat.

The discipline — one change per experiment, scored against a fixed bar, kept or reverted — is
what makes it work. It removes the activation energy of running one more iteration and stops
"while I'm here, let me also..." edits that make it impossible to tell what actually helped.

## This skill = loop + rubric

- **The loop** (this file) is universal. It does not care what you are writing.
- **The rubric** (a separate file) is genre- and voice-specific. It defines the dimensions,
  the anti-patterns, and the calibration anchors that say what 5/5 looks like *for this kind
  of writing in this voice*. A generic rubric scores everything a bland 3/5 and reverts
  nothing useful — the calibration is the whole point.

**Resolving the active rubric**, in order:
1. If `references/rubric.md` exists, use it. (Your local, voice-calibrated rubric — gitignored.)
2. Else if a bundled example rubric exists in `references/` (e.g.
   `references/rubric.waglesworld-blog.md`), use it — but tell the user it is calibrated to a
   specific voice/genre and offer to help build their own from `references/rubric.example.md`.
3. Else ask the user for their rubric, or walk them through `references/rubric.example.md`.

Never invent dimensions on the fly. If there is no rubric, stop and get one — an unscored
loop is just freestyling.

## Modes

Pick the mode from how you were invoked. If unclear, ask which.

### Chat mode (no file access — pasted draft)
Use when the draft is pasted into the conversation and you cannot edit files.
- The **conversation history is the snapshot.** Before each change, restate the current
  version (or the paragraph you are changing) so a revert is just "go back to the prior text."
- Propose ONE change, show the before/after, re-score, give the verdict. On KEEP, the new
  text becomes current. On REVERT, discard it and keep the prior text.
- At the end, output the final text in full plus the experiment log.

### File mode (agent with file tools — path to a draft)
Use when given a path to a draft file.
- Before each change, snapshot: copy the draft to `<draft>.snapshot-N.md`.
- Edit the file in place, ONE change only.
- On REVERT, restore the file from the latest snapshot.
- At the end, leave the improved file plus the snapshots (for diff review) and the log.

## Workflow

1. **Read the draft.** (Chat: read the pasted text. File: `view` the path.)
2. **Resolve the rubric** (see above). Load its dimensions, anti-patterns, calibration anchors.
3. **Identify the spine/structure FIRST.** Before scoring, decide which structural pattern the
   piece uses — the rubric lists the valid ones. This sets what 5/5 means for the
   structure-dependent dimensions. Don't penalize a piece for lacking a move its spine
   doesn't need.
4. **Initial scoring.** Score every dimension 1–5. Print a table: dimension, score, one-line
   justification. Print the total (e.g. `/45` for a 9-dimension rubric).
5. **Pick the lowest-scoring dimension.** Break ties using the rubric's stated tie-order.
6. **Propose ONE targeted change.** State the hypothesis explicitly: "Dim X is at 2 because Y.
   Change: rewrite paragraph N to do Z. Predicted: X → 4."
7. **Snapshot** (file mode) or **restate current text** (chat mode).
8. **Make the change.** ONE change. No bundled improvements.
9. **Re-score the changed dimension AND scan anti-patterns globally.** If any anti-pattern
   appeared anywhere in the piece → **HARD REVERT**, regardless of the score delta.
10. **Verdict:**
    - Score improved AND no anti-pattern introduced → **KEEP.** Log it. Continue.
    - Score same or lower, or an anti-pattern appeared → **REVERT.** Log it. Try a different
      dimension, or a different approach to the same one.
11. **Loop until a stop condition hits.**

## Stop conditions

- Total score reaches the rubric's target (e.g. ≥ 40/45), or
- 3 consecutive REVERTs (you are out of productive moves for now), or
- 10 experiments total, or
- the user says stop.

## Critical rules

- **Identify the spine before scoring.** Score a piece against the bar for the structure it
  is actually using.
- **ONE change per experiment.** Never bundle. Isolating what helped is the entire method.
- **Anti-patterns are hard reverts.** Do not negotiate. The score delta is necessary but not
  sufficient.
- **Comparative dimensions use pairwise comparison.** For a dimension like "taste" that can't
  be scored solo, compare changed-vs-prior against the calibration anchor; if it's a tie,
  REVERT.
- **No narration of routing decisions.** Just start scoring.
- **No emojis** in output unless requested.
- **Never claim a change "improved the piece" without showing the score delta.**

## Output

After each experiment, append a row to the experiment log:

```
| # | Dim Targeted | Change | Score Δ | Verdict |
|---|---|---|---|---|
| 1 | Earned Reveal (2→?) | Rewrote opener to state the prior hypothesis explicitly | +2 (2→4) | KEEP |
| 2 | Taste | Added "everyone knows this by now" to the opening | n/a | REVERT (reader-flattery anti-pattern) |
```

At the end:
- Final score table: dimension | initial | final | delta
- The full improved text (chat mode) or path to the final draft + snapshots (file mode)
- The complete experiment log

---

*Adapted from [mavaali/autoresearch-writing](https://github.com/mavaali/autoresearch-writing) (MIT © Mihir Wagle), generalized from blog drafts to any writing with a pluggable rubric and a chat/file dual mode. That work itself derives from Andrej Karpathy's [autoresearch](https://github.com/karpathy/autoresearch) and Irina Gorbach's adaptation of the loop for article editing. See [CREDITS](../CREDITS.md).*
