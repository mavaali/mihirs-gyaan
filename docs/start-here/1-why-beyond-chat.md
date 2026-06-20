# Why bother going beyond chat?

When you chat with an LLM, you re-explain yourself every time. You know *how* you want it to
work — challenge my assumptions, cite sources, don't hedge, follow this structure — but you
have to say it again in every conversation, and it half-listens.

A **skill** is that "how" written down once, so the model follows it consistently. Same job,
same rigor, every time. You stop being a prompt typist and start being someone who *runs a
process*.

## The one idea

> A skill turns "be helpful" into "do *this specific job* the *right way*."

Chat optimizes for a pleasant answer. A skill optimizes for a *correct outcome* — and it will
push back, ask first, refuse to skip steps, or revert its own work to get there.

## Before / after

**You write code. You ask chat: "Should I build a caching layer here?"**
- *Vanilla chat:* "Great idea! Here's how to build one..." — it agrees and starts coding.
- *With the [brainstorming](../../brainstorming) skill:* "Before that — is caching the right
  problem, or is the query slow because of an N+1? What does this displace?" — it challenges
  the premise before letting you build the wrong thing.

**You don't write code. You ask chat: "Why does my team keep missing deadlines?"**
- *Vanilla chat:* a tidy list of five generic reasons, all plausible, none tested.
- *With the [causal](../../causal) skill:* it forces a chain — effect → mechanism →
  conditions → environment check → alternatives — and makes you reject your first guess before
  settling on a cause.

Same model. The difference is the *discipline* the skill imposes. That's the whole game.

---

> [!TIP]
> **Try this (no setup):** Open any chat box and ask it to "improve this paragraph," pasting a
> few sentences you wrote. Notice what it does — it tightens words but has no *standard* it's
> measuring against. Hold that feeling. On the [next page](./2-first-win.md) you'll give it a
> standard and watch it behave completely differently.
>
> **You'll know it worked when:** you can name what the vanilla edit was missing (a rubric, a
> bar, a reason to revert a change).
