# Design: Getting-Started On-Ramp for mihirs-gyaan

**Date:** 2026-06-20
**Status:** Design approved, not yet implemented
**Scope decision:** Hold (full sequenced on-ramp; skills untouched; additive `docs/` tree)

## Problem

The repo is a clean library of portable agent skills — optimized for *scanning and
copying*. It has no on-ramp for someone whose only reference point is using an LLM as a
chat sidebar. We want a guided path that takes a newcomer from "I only chat" to "I run
skills," using the skills themselves as the teaching material — without dissolving the
library that already works.

## Audience

**Both, with one fork.** Two first-class lanes that share an entry:

- **Coders** — developers who use ChatGPT/Claude as a chat sidebar but haven't adopted
  agentic/skill workflows.
- **Knowledge workers** — non-coders who only chat.

The knowledge-workers lane is **newer and growing** (more general-knowledge skills are
planned). The guide presents it as a first-class lane — "here's what's ready now" — not
an apology for a coder-heavy corpus. Adding skills later must drop in as *rows*, never a
restructure.

## Desired outcome

A sequenced arc: **mindset → first hands-on win → pick your lane → setup → curated path.**

## The reframe (why not a literal "guide")

Converting the repo *into* a getting-started guide would bury its only moat — the actual
skills — under commodity "intro to AI agents" content. Instead: **add a guided on-ramp
that uses the skills as the teaching vehicle.** The skills stay the star; the guide is the
doorway, not the building. Everything lives under `docs/start-here/`; no skill content
moves.

## Design

### A. Generalize `autoresearch-writing` into the corpus

Pull https://github.com/mavaali/autoresearch-writing in and expand it from blogs to **any
writing**.

- **Core insight:** the Karpathy-style editing *loop* (score on a rubric → one change per
  experiment → snapshot → keep/revert → anti-patterns are hard reverts → stop conditions)
  is **universal**. The **rubric is the pluggable part** — it is what is genre- and
  voice-specific.
- **Do NOT** flatten the rubric into a generic one. A generic rubric scores everything a
  bland 3/5 and reverts nothing useful. *A generic rubric displaces the voice-calibration
  that is the skill's entire edge.*
- **Pluggable rubric:** ship the existing blog rubric as the default `rubric.md`, plus a
  `rubric.example.md` the user swaps per genre/voice. Populated copies stay local
  (gitignored), mirroring the corpus's `*.example.md` convention.
- **Dual mode** (new generalization axis beyond genre):
  - **Chat mode** — paste a draft into any chat box; the model scores, proposes ONE
    change, the user says keep/revert; the conversation history *is* the snapshot. No file
    ops. Works for a pure chat-only newcomer.
  - **File mode** — the original automated loop; needs a CLI agent; writes
    `<draft>.snapshot-N.md`.
- **Provenance:** carry forward the upstream credit (Karpathy `autoresearch` + Irina
  Gorbach's adaptation) into both the skill and root `CREDITS.md`.

This skill is the **shared first win** for both lanes — everyone writes, and a disciplined
scored editing loop is a far stronger demo than "make it better." Its dual mode is also the
guide's spine: *same skill, manual in chat, automated once you have an agent* — the
chat→agent graduation made concrete.

### B. The guide (`docs/start-here/`)

```
docs/start-here/
  README.md            # index; routes newcomer vs. browser; entry to the arc
  1-why-beyond-chat.md # shared mindset; TWO before/afters (one coding, one not)
  2-first-win.md       # SHARED: autoresearch-writing in CHAT mode on a draft you have
  3-go-deeper.md       # forks: "Do you write code?"
                       #   coders → brainstorming + Track A
                       #   knowledge workers → causal, meeting-synthesizer + Track B
  track-a-cli-agent.md # host-neutral: Claude Code OR Codex; where each loads skills;
                       #   then gstack-*, debugging-vite-apps, get-api-docs, requirements-builder
  track-b-notes-vault.md # Obsidian; fresh-vault scaffold OR existing-vault branch;
                       #   then daily/weekly/monthly/quarterly, journal-process, notebooklm
  the-full-map.md      # whole corpus by tier + setup each needs (skills land here as rows)
```

**README top** gets two doors above the existing skill tables:
> **New to this?** → Start with the [guide](./docs/start-here). **Just want a skill?** →
> Jump to [Skills](#skills).

**First wins:**
- Both lanes start with `autoresearch-writing` (chat mode), on a draft the reader already
  has. The page scripts the *exact* paste and first turn — no hand-waving.
- The fork happens after the first win, in `3-go-deeper.md`.
- Coders then meet `brainstorming` (framed honestly as a coding design skill: "before you
  build, paste this").
- Knowledge workers meet `causal` ("why does my team keep missing deadlines?") and
  `meeting-synthesizer` (needs transcripts → a natural 2nd win).

**Host-agnostic throughout:** never "install Claude Code" as the only door. Track A offers
Claude Code *or* Codex (or any agent that loads `SKILL.md`).

### C. Existing-vault handling (Light branch — no skill edits)

`track-b-notes-vault.md` branches:
- **Fresh/empty vault** → copy-paste the skill-ready folder scaffold (below).
- **Existing structured vault** → "these planning skills expect these folder names; either
  add them, or open each skill's `## Vault Paths` block and rewrite the paths to match your
  vault." Leverages the editable block already at the top of every planning skill.

Skill-ready scaffold (union of paths the skills reference):
```
$VAULT_ROOT/
  fleeting/  literature/  ideas/          # daily-process
  reflections/
    weekly/                               # weekly/monthly/quarterly/journal-process
    <YEAR>-plan/                          # weekly/monthly/quarterly  (see year-hardcoding nit)
  writing/
    editorial-calendar.md
    ideas/inbox.md
    drafts/                               # monthly-plan
  templates/
    weekly-reflection.md                  # weekly-plan (optional)
    notebook-source.md  dashboard.md      # notebooklm (see casing nit)
```

## What already exists (reuse, don't rebuild)

- 15 portable skills + the (to-be-added) generalized `autoresearch-writing`.
- `CREDITS.md` + per-skill attribution footers (housekeeping PR #3).
- Standardized frontmatter `{name, description, optional user-invocable}` documented in
  README (PR #3).
- `*.example.md` "fill-in-your-own" convention (meeting-synthesizer) — reused for the
  pluggable rubric and the vault config story.
- Every planning skill already has an editable `## Vault Paths` block — reused for the
  existing-vault branch.

## Failure-mode check

- **Succeeds wildly:** the writing first-win pulls in non-writers too — fine; the fork
  still routes everyone to their lane.
- **Fails:** if the chat-mode loop feels clunky, the first impression dies. Mitigation:
  `2-first-win.md` must script the literal paste + expected first turn, not describe it.
- **6-month:** a new skill is new maintenance; the pluggable rubric prevents it rotting
  into your-voice-only. The two-lane structure absorbs new knowledge skills as rows.

## NOT in scope

- **Vault-config refactor** (shared variable mapping so planning skills read paths from one
  file instead of hardcoding) — deferred; the Light existing-vault branch covers users now.
- **Year-hardcoding fix** (`reflections/2026-plan/` in 5 planning skills) — known nit;
  scaffold uses `<YEAR>` placeholder, skills unchanged for now.
- **`notebooklm` template casing** (`Templates/Types/` vs `templates/`) — known nit; reconcile separately.
- **Per-skill difficulty/setup badges and a graduation diagram** — Expand-tier polish;
  add later if the guide proves out.
- **Non-Obsidian vault walkthroughs** (Logseq, plain Markdown) — mention as supported,
  don't write full guides yet.

## Open follow-ups (separate work)

1. Generalize + import `autoresearch-writing` (skill work; precedes the first-win page).
2. Build `docs/start-here/` pages.
3. README top-of-file routing.
4. (Later) vault-config refactor; year + casing nits; badges/diagram.
