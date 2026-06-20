# Your first win

You'll run the [autoresearch-writing](../../autoresearch-writing) skill on something you
already wrote — an email, a paragraph, a post, anything. It scores your draft on a rubric,
changes **one thing**, checks whether the score went up, and keeps or reverts. Then again.
This is the "first win" because everyone writes, and the difference from "make it better" is
immediate.

No install. You'll run it in **chat mode**: the conversation itself is the safety net (every
version is right there in the scrollback), so nothing can be lost.

## Do this (≈10 minutes)

**1. Open any chat box** — claude.ai, ChatGPT, or a CLI agent like Codex. Whatever you have.

**2. Paste the skill, then your draft.** Copy the whole of
[`autoresearch-writing/SKILL.md`](../../autoresearch-writing/SKILL.md) and
[`references/rubric.waglesworld-blog.md`](../../autoresearch-writing/references/rubric.waglesworld-blog.md),
then send this:

> Follow the instructions in this SKILL.md. Use the rubric below. Run in **chat mode** on my
> draft. Score it, then do one experiment at a time and ask me before each change.
>
> --- SKILL.md ---
> *(paste SKILL.md)*
>
> --- RUBRIC ---
> *(paste rubric.waglesworld-blog.md)*
>
> --- MY DRAFT ---
> *(paste your draft)*

> [!NOTE]
> The bundled rubric is calibrated to one person's blog voice — perfect for *seeing the loop
> work*. Once you've felt it, [build your own rubric](../../autoresearch-writing/references/rubric.example.md)
> for your genre and voice (that's the capstone exercise).

**3. Read the opening score table.** It looks like this:

```
| # | Dimension          | Score | Why                                          |
|---|--------------------|-------|----------------------------------------------|
| 1 | Earned Reveal      | 2/5   | Opener states a topic, not a tension         |
| 5 | Headings as Claims | 2/5   | "Background", "Details" — labels, not claims |
| 7 | Landed Claims      | 3/5   | Two hedges ("might", "I think") leak in      |
| ...                                                                       |
Total: 27/45
```

**4. Let it run one experiment.** It picks the lowest dimension, states a hypothesis ("Dim 5
is at 2 because the headings are labels; rewrite them as claims; predict 2→4"), makes *one*
change, re-scores, and gives a verdict: **KEEP** or **REVERT**.

**5. Watch a revert happen.** Sooner or later a change won't help, or it'll trip an
anti-pattern (say, it sneaks in an em dash). The skill reverts it and tells you why. *That's
the moment* — it's not just generating, it's running disciplined experiments and throwing away
what doesn't work.

## What just happened

You gave the model a **standard** (the rubric) and a **method** (one change, measured, kept or
reverted). It stopped guessing and started optimizing toward something checkable. That's a
skill.

---

> [!TIP]
> **Try this:** Run the loop until it KEEPs at least one change *and* REVERTs at least one.
>
> **You'll know it worked when:** a dimension score actually went up between turns, **and** you
> watched it discard a change that didn't help (or broke an anti-pattern). If everything was a
> KEEP, your draft was already strong — paste a rougher one and try again.

When you want this to run *automatically on a file* — snapshotting and editing in place
instead of you approving each turn — that's the next step. → **[Go deeper](./3-go-deeper.md)**
