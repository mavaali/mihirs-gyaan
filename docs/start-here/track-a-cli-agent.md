# Track A — Set up a CLI agent

A CLI agent runs in your terminal, reads your files, and *does* things — edits code, runs
tests, opens PRs. It loads skills from a folder. These skills are host-agnostic: pick whatever
agent you like.

## Pick an agent

| Agent | Where skills live | Notes |
|-------|-------------------|-------|
| **Claude Code** | `~/.claude/skills/<name>/` (global) or `.claude/skills/` (per-project) | Drop a skill folder in; invoke by describing the task |
| **Codex** | per its skills/instructions config | Same skill files; point it at the `SKILL.md` |
| **Any other agent** | wherever it reads instruction files | If it can read a `SKILL.md` and follow it, these work |

> [!NOTE]
> Nothing here says "you must use Claude Code." A skill is just Markdown. The only requirement
> is an agent that can read a `SKILL.md` and act on your files.

## Install your first skill

1. Copy a skill folder into your agent's skills location. Start with
   [`brainstorming`](../../brainstorming):

   macOS / Linux:
   ```
   cp -r brainstorming ~/.claude/skills/        # Claude Code example
   ```
   Windows (PowerShell):
   ```
   Copy-Item -Recurse brainstorming $env:USERPROFILE\.claude\skills\
   ```
2. If the skill has a `references/*.example.md`, copy it to the non-`example` name and fill it
   in. (Populated copies stay local — they're gitignored.)
3. Invoke by describing the task — the agent matches the skill's `description`.

## Run one end-to-end

The cleanest first run is the skill you already met, now in **file mode**:

- Point your agent at a real draft file and ask it to run
  [`autoresearch-writing`](../../autoresearch-writing) on it.
- This time it snapshots the file (`<draft>.snapshot-N.md`), edits in place, and reverts by
  restoring a snapshot — no approving each turn. Same loop, automated.

Then graduate into the dev tier:
[`requirements-builder`](../../requirements-builder) → [`debugging-vite-apps`](../../debugging-vite-apps)
→ [`get-api-docs`](../../get-api-docs) → [`gstack-ship`](../../gstack-ship) (and friends).

---

> [!TIP]
> **Try this:** Before your next real change, run [`brainstorming`](../../brainstorming) in your
> agent: "Use the brainstorming skill — I want to build X."
>
> **You'll know it worked when:** it challenged your premise at least once and produced a short
> design doc *before* any code. A skill ran outside a chat box, on your project.

← back to [Go deeper](./3-go-deeper.md) · see [The full map](./the-full-map.md)
