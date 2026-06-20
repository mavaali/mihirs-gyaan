# Track B — Set up a notes vault

The notes, journaling, and planning skills work *with your knowledge* — so they need a place
to read and write: a **vault**. A vault is just a folder of Markdown files. We'll use
[Obsidian](https://obsidian.md) (free) because it's the smoothest, but any Markdown folder
(Logseq, plain files) works — the skills reference a `$VAULT_ROOT`, never a hardcoded path.

## 1. Install Obsidian, make a vault

Download Obsidian, click **Create new vault**, name it, pick a folder. That folder is your
`$VAULT_ROOT`. Done — that's the whole install.

## 2. Set up the folders — pick your situation

### Fresh / empty vault → use this scaffold

The planning skills expect a few folders. Create them once and the skills work out of the box.
From your vault root:

```
$VAULT_ROOT/
  fleeting/                     # daily-process: quick captures
  literature/                   # daily-process: notes from things you read
  ideas/                        # daily-process
  reflections/
    weekly/                     # weekly-plan, journal-process  → MM.DD.YY-MM.DD.YY.md
    <YEAR>-plan/                # weekly/monthly/quarterly plans → e.g. 2026-plan/
  writing/
    drafts/                     # monthly-plan
    ideas/                      # monthly-plan (inbox.md lives here)
    editorial-calendar.md       # monthly-plan
  templates/
    weekly-reflection.md        # optional; weekly-plan falls back to a built-in format
```

> [!NOTE]
> Replace `<YEAR>` with the current year (e.g. `reflections/2026-plan/`). A few planning skills
> currently spell the year out in their paths — match it, or edit the skill's path (next
> section) if you prefer a year-less layout.

Quick create (macOS/Linux), run from your vault root:
```
mkdir -p fleeting literature ideas reflections/weekly "reflections/$(date +%Y)-plan" writing/drafts writing/ideas templates
```

### Already have a structured vault → point the skills at it

Don't reorganize your vault to match ours. Instead, tell each skill where *your* folders are.
Every planning skill has a **`## Vault Paths`** block at the top of its `SKILL.md`:

```
## Vault Paths
- **Vault root:** ...
- **Weekly reflections:** reflections/weekly/[MM.DD.YY]-[MM.DD.YY].md
- ...
```

Open the skills you want ([daily-process](../../daily-process), [weekly-plan](../../weekly-plan),
[monthly-plan](../../monthly-plan), [quarterly-plan](../../quarterly-plan),
[journal-process](../../journal-process)) and rewrite those path lines to match your existing
folders. That's the only change needed — the logic reads from that block.

## 3. Run one end-to-end

Point your agent at your vault (set `$VAULT_ROOT`) and run
[`daily-process`](../../daily-process) on a day's worth of notes, or
[`causal`](../../causal) on a real recurring problem (causal needs no vault — pure chat).
A natural second win is [`meeting-synthesizer`](../../meeting-synthesizer) once you have a
couple of meeting transcripts.

---

> [!TIP]
> **Try this:** Run [`causal`](../../causal) on a real recurring annoyance ("why does X keep
> happening?").
>
> **You'll know it worked when:** it walked the five-step chain and made you *reject your first
> guess* before landing on a cause. Then scaffold your vault and run one planning skill on real
> notes.

← back to [Go deeper](./3-go-deeper.md) · see [The full map](./the-full-map.md)
