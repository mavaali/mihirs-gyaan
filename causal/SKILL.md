---
name: causal
description: |
  Pearl-discipline causal harness for debugging, diagnosis, and "why did X happen" questions. Forces a five-step chain (Effect → Mechanism → Conditions → Environment Check → Alternatives) before settling on any causal explanation, to prevent jumping from observation to single-link cause.

  Use when the user asks "why did X happen", "what's causing this", "why is X broken", "why does this keep happening", "diagnose this", "root cause", or presents a crash/error/anomaly/behavior pattern that demands explanation. Also use when YOU would otherwise produce a single-link causal claim ("X is broken because Y is buggy") — engage this skill instead.

  Do NOT use for: simple factual lookups ("what is X"), how-to questions ("how do I do X"), forward-looking planning ("what should I do"), or questions where causation is trivially obvious and the user wants only a one-line answer. Lightweight curiosity questions ("why is the sky blue") do not need this — only engage when a wrong causal explanation would actually cost the user something.
---

# Causal — Pearl-discipline reasoning harness

You are about to produce a causal explanation. Stop. Run the five-step chain below before stating any conclusion. This skill exists because the most common reasoning failure is jumping from **effect** directly to a **single plausible cause** without checking the mechanism or the environment.

## The Five Steps

Run these in order. Do not skip. If you cannot complete a step, say so explicitly rather than fabricating.

### 1. Effect — what is actually observed

State the observation in neutral, mechanism-free language. No interpretation. No "X is broken" — describe what the user/system sees.

- What happened?
- When (sequence, timing, frequency)?
- Under what conditions does it appear / disappear?
- What is the smallest reliable reproduction?

If the effect is fuzzy or anecdotal, name that. Do not proceed to mechanism on a vague effect.

### 2. Mechanism — what causal pathway would produce this effect

Force a multi-link chain, not a single-word cause. The shape is:
> "X does Y, which depends on Z; Z fails when W; therefore the effect appears."

Three rules:
- **No single-link causes.** "It's a bug in the client" is not a mechanism. "The client's stop path reads from XPC, that read fails when no data is buffered, the unhandled exception aborts the process" is a mechanism.
- **No labels-as-causes.** "Race condition" / "config drift" / "network issue" are categories, not mechanisms. Spell out the actual sequence.
- **Mechanism must be falsifiable.** If you wrote one, you should be able to name a test or observation that would disprove it.

If you genuinely don't know the mechanism, say so. Then either: (a) ask the user a targeted question that would resolve it, or (b) propose 2–3 candidate mechanisms and proceed to test each through steps 3–5.

### 3. Conditions — what must be true upstream for the mechanism to fire

For the mechanism you named, enumerate the upstream conditions it requires. This is the most-skipped step. It is the one that catches the actual root cause.

Ask: "for the mechanism in step 2 to produce the effect in step 1, what state of the world must hold?"

Examples of condition categories:
- **Environmental state** (DNS settings, network type, OS version, installed extensions)
- **Configuration** (user settings, profiles, feature flags, recent changes)
- **Other actors** (other processes, other people, other systems touching the same surface)
- **Temporal** (what changed recently, what's different from the last working state)
- **Resource state** (memory, disk, handles, sockets, quotas)

You are looking for conditions that are *plausibly variable* across "working" and "broken" cases. Do not list constants.

### 4. Environment Check — which of those conditions actually hold here

For each condition from step 3, check whether it holds in the user's actual situation. Use available tools (bash, file read, web, the user's own answers) to verify, not to guess.

Three outcomes per condition:
- **Confirmed present** — evidence shows it holds. This is a candidate root cause.
- **Confirmed absent** — evidence shows it does not hold. Rule out.
- **Unknown** — cannot verify with current information. Either ask the user, or flag as a gap.

If you find a confirmed-present condition that matches the mechanism, you have a candidate root cause. Do not stop yet — continue to step 5.

### 5. Alternatives — what other mechanisms could produce the same effect

Generate ≥2 alternative mechanisms that would produce the same effect. For each:
- Briefly state the mechanism
- Name a condition that would distinguish it from your primary
- Check whether that condition holds

This is the anti-confirmation-bias step. If your primary mechanism is correct, the alternatives should be rule-out-able with evidence. If you cannot distinguish your primary from alternatives, your confidence should drop, not increase.

## Output format

Produce the analysis with these exact section headers, in this order:

```
## Effect
[Step 1 — observation in neutral language]

## Mechanism
[Step 2 — causal chain, multi-link, falsifiable]

## Conditions required
[Step 3 — bulleted list of upstream conditions the mechanism needs]

## Environment check
[Step 4 — for each condition: Confirmed / Absent / Unknown, with evidence]

## Alternatives considered
[Step 5 — ≥2 alternative mechanisms with distinguishing tests]

## Conclusion
[The candidate root cause, with a confidence qualifier: High / Medium / Low and why]
```

Keep each section tight. The goal is forcing the discipline, not generating prose. A good output for a simple problem is short.

## Critical rules

- **No single-link causes.** "It's broken because of X" is not a mechanism. Always spell the chain.
- **Mechanism before condition before evidence.** Do not start enumerating environment state until you have stated the mechanism. Otherwise you are pattern-matching, not reasoning.
- **No vendor-bug shortcuts.** Before concluding "this is a bug in [vendor], file a ticket," you must have completed steps 3 and 4 and found at least one alternative mechanism in step 5 that you can rule out. A vendor bug is a legitimate conclusion — but only after the environment has been checked, not as a substitute for checking it.
- **Confidence must match evidence.** If you completed all five steps cleanly, you can claim High. If you skipped a step or have Unknowns, you cannot.
- **State the skipped step.** If you can't complete a step (lack of access, lack of time, lack of information), say "step N skipped because Y" — do not silently pretend you did it.

## When this skill should not engage

- Factual lookups ("what is the VPN client version") — answer directly
- How-to questions ("how do I install X") — answer directly
- Trivial-causation questions ("why won't this start — oh, it's not plugged in") — one-shot it
- Forward-looking planning ("should I refactor this") — different skill (decision-making, not causal)
- Curiosity questions where being wrong has no cost — answer at appropriate depth

The cost of running this skill on a too-small question is verbosity. The cost of not running it on a real diagnostic question is jumping to a wrong cause. Use judgment.

## Reference material

For deeper background, mechanism generators, and worked examples, see:
- `references/pearl-discipline.md` — the philosophy and why this works
- `references/mechanism-generators.md` — prompts to force non-obvious mechanisms when stuck
- `references/examples/` — worked examples across debugging, behavioral, decision domains
