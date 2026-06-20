# Pearl discipline — why this five-step chain works

## The failure mode this prevents

The default reasoning failure is **single-link causation**. Effect happens → first plausible cause comes to mind → declare that the cause → stop. This is fast and usually wrong in non-trivial cases.

Judea Pearl's framework (from *The Book of Why*) gives a stricter discipline: causation requires a **mechanism**, mechanisms have **conditions**, and conditions live in the **environment**. To make a causal claim, you must trace the chain from effect back through mechanism, through conditions, into the actual environment. Anything less is correlation dressed up as causation.

## Why each step matters

### Step 1 (Effect) catches: overconfident framing
If you describe the effect as "the client is broken," you have already smuggled in a partial cause ("the client"). Neutral framing ("internet stops working when this app is active") keeps the search space open.

### Step 2 (Mechanism) catches: label-as-cause
"It's a memory leak," "it's a race condition," "it's a config issue" are categories, not explanations. A real mechanism describes the *actual sequence of operations* that produces the effect. If you cannot describe the sequence, you do not yet have a mechanism — you have a guess shaped like one.

### Step 3 (Conditions) catches: the actual root cause
Most failures are environment-conditional. The same code works for one user and breaks for another because some upstream condition differs. If you skip enumeration of conditions, you skip the place where the answer lives.

This is the step models skip most often. It feels redundant because the mechanism "obviously" implies its conditions. But making them explicit forces you to ask: which of these is variable? Which has the user changed recently? Which differs from a known-working baseline?

### Step 4 (Environment Check) catches: assumption-as-fact
Once conditions are explicit, you can *check* them. Tools (bash, file reads, web, asking the user) become productive because you know what to look for. Without step 3, environment checks are random fishing.

### Step 5 (Alternatives) catches: confirmation bias
The first mechanism you find that matches the evidence is rarely the only one that would match. Forcing alternatives — and forcing distinguishing tests — prevents the very human move of locking onto the first plausible answer.

## The Pearl ladder, briefly

Pearl describes three rungs of causal reasoning:

1. **Association** — "X and Y happen together." (Correlation.)
2. **Intervention** — "If I change X, Y changes." (Mechanism, falsifiable.)
3. **Counterfactual** — "If X had not happened, Y would not have happened." (Strongest claim.)

This skill operates primarily at rung 2 (mechanism + intervention) and uses rung 3 for the alternatives step (counterfactual: "if this alternative were the real cause, what would we see instead?").

## When the discipline fails

This harness is not magic. It fails when:

- **The user's environment is invisible.** If you cannot inspect their system, you cannot check conditions. Ask, or flag the gap honestly.
- **The mechanism space is genuinely unknown.** For novel failures with no prior art, you may not be able to generate a mechanism. Say so. Propose candidates and test through evidence rather than reasoning.
- **The answer is at a lower level than you can reach.** Some causes live in code you cannot read. The discipline still helps — it narrows the search — but the final answer may require escalation.

What the discipline *always* does, even when it fails to find a root cause, is prevent confident wrong answers. That is the floor it guarantees.

## A note on speed

Running the full five-step chain on every question is not the goal. The goal is to run it when the question matters — when jumping to a wrong cause would waste the user's time, mislead them, or hide a real underlying issue.

For trivial diagnosis, a one-shot answer is fine. The skill description above gives criteria for when to engage. Use judgment.
