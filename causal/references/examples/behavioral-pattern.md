# Example: "Why do I keep missing my Friday writing time?"

A worked example showing the skill applied to a behavioral / personal pattern. Different domain from debugging, same discipline.

## Setup

User says: "I keep blocking off Friday afternoons for writing, and I keep losing the time to other work. Why does this keep happening?"

## Before (single-link causation — weak)

> "You're not protecting the time well enough. Try harder. Decline more meetings."

Single-link: "lack of discipline → lost time." Not actionable, not falsifiable, almost certainly wrong.

## After (five-step chain)

### Effect
- User blocks Friday 1–5pm for writing on their calendar
- Over the last 6 weeks, writing happened in that block 1 time
- The block is "lost" in two patterns: (a) meeting requests get accepted into it, (b) it stays free on the calendar but the user does email/Slack instead
- The user notices the pattern and feels frustrated about it
- The user does write — successfully — at other times (early mornings, weekends), just not in this block

### Mechanism
Two candidate mechanisms, possibly co-occurring:

**Mechanism A (meeting capture):** Friday afternoon is a low-friction meeting slot for the rest of the org (end of week, people want to close loops). When meeting requests arrive, the user's default response is to accept rather than counter-propose, because the "writing" label on the block doesn't carry the same weight as a meeting commitment. The block gets eaten meeting by meeting.

**Mechanism B (energy depletion):** By Friday afternoon, the user is at the lowest-energy point of the week. Writing is a high-cognitive-load task. When the body is depleted, it routes to low-cognitive-load tasks (email, Slack) even when the calendar says "write." The block stays nominally free but is functionally unavailable.

### Conditions required

For Mechanism A:
- The user must be accepting meeting invites into the block (vs. declining/counter-proposing)
- The block's label must not be commitment-shaped in the user's own framing
- Friday afternoon must in fact be a high-request slot from peers

For Mechanism B:
- Friday afternoon must be a low-energy time for this user specifically
- The user must default to low-cognitive-load work when depleted
- The writing task must require energy the user doesn't have at that hour

### Environment check
For A:
- Look at the user's actual calendar for the last 6 Fridays: how many meeting invites landed in the 1–5pm slot? How many did the user accept vs. decline?
- Did the user use the "tentative" or "decline with counter-propose" option for any of them?

For B:
- When does the user successfully write? (Early mornings, weekends — both rested states.)
- What does the user *actually* do during the lost block? (If: email/Slack → matches B. If: meetings → matches A.)
- Ask the user: on a Friday at 1pm, are they tired? Wired? Anxious about the weekend?

### Alternatives considered

1. **The writing project itself is aversive.** User avoids the block because the work feels hard, not because of energy or meetings. Distinguishing test: does the user write on Fridays if they happen to have nothing else planned? If "no, still avoid," this is the real mechanism.
2. **The block is too long.** Four hours of writing is a longer commitment than the user can actually sustain. They never start because the size is intimidating. Distinguishing test: would a 90-minute block on Friday morning get used?
3. **The calendar block is performative.** User blocks the time to signal commitment to themselves but doesn't actually intend to use it. Distinguishing test: would the user move the block to a different day if asked to defend it?

### Conclusion
Candidate root cause depends on environment check. Most likely a combination of A + B: meetings eat some Fridays, energy depletion eats the rest. The "lack of discipline" framing is wrong because the user successfully writes at other times — discipline isn't the variable.

**Recommendation:** Don't try harder. Either (a) move the block to a high-energy time (early Friday morning, or move it off Friday entirely), or (b) explicitly make the block decline-by-default for meetings and verify the energy hypothesis holds.

**Confidence: Medium** — until environment check is run, both mechanisms are plausible and the recommendation differs by which dominates.

## Why this matters

The single-link "lack of discipline" answer would have led to more willpower investment, which would have failed, which would have produced shame and another lost block. The chain produces an answer that's actionable *and* doesn't pathologize the user.

The skill is not just for technical debugging. The discipline transfers anywhere causal explanations matter.
