# Mihir's Gyaan

> *Gyaan* (ज्ञान) — knowledge. A small, growing corpus of portable agent skills.

A collection of **agent skills** — self-contained instruction sets that teach an AI assistant
how to do a specific job well. They're plain Markdown (`SKILL.md` + optional `references/`),
so they work with any agent that can load skill files.

> **New to this?** Start with the **[guide](./docs/start-here)** — go from "I only chat with an
> LLM" to running skills, with a hands-on first win in ~10 minutes (no install).
> **Just want a skill?** Jump to **[Skills](#skills)** below.

## Works with

These skills are model- and host-agnostic. They've been used with:

- **Claude Code** — drop a folder into your skills directory
- **Claude Desktop / claude.ai** — load as a project skill
- **Microsoft Scout / Copilot CLI** — install as an `m-skill` or reference the `SKILL.md`
- Any agent that can read a `SKILL.md` and follow it

The reasoning skills (`meeting-synthesizer`, `causal`, `brainstorming`, `requirements-builder`)
are **pure instructions** — zero setup, fully portable. A few skills assume specific tools
(see each skill's README); those are portable in design but need light configuration.

## Skills

### Reasoning & analysis (zero-setup, fully portable)
| Skill | What it does |
|-------|--------------|
| [meeting-synthesizer](./meeting-synthesizer) | Cross-meeting synthesis of a transcript series — decisions, action items, leadership signals, conflict detection |
| [causal](./causal) | Pearl-discipline causal harness — forces a five-step chain before settling on any "why did X happen" explanation |
| [brainstorming](./brainstorming) | Structured ideation before creative work — diverge, then converge, before building |
| [requirements-builder](./requirements-builder) | Turn a feature idea into user stories with acceptance criteria, edge cases, and scope boundaries |

### Writing & craft (portable; bring a rubric)
| Skill | What it does | Needs |
|-------|--------------|-------|
| [autoresearch-writing](./autoresearch-writing) | Karpathy-style editing loop — score a draft on a rubric, make one change per experiment, keep or revert. Works on any writing, in a chat box or with a file-editing agent | A rubric (a worked example ships; copy [`rubric.example.md`](./autoresearch-writing/references/rubric.example.md) to make your own) |

### Dev & shipping (need a project + tooling)
| Skill | What it does | Needs |
|-------|--------------|-------|
| [debugging-vite-apps](./debugging-vite-apps) | Diagnose blank pages, runtime crashes, and module errors in Vite/bundler-served apps | A Vite app |
| [get-api-docs](./get-api-docs) | Fetch authoritative docs for a library/SDK/API before writing code against it | Web access |
| [gstack-browse](./gstack-browse) | QA / dogfooding via browser automation — navigate, interact, assert, screenshot | Browser automation |
| [gstack-qa](./gstack-qa) | Systematically QA a web app and file bugs with evidence | Browser automation |
| [gstack-ship](./gstack-ship) | Ship workflow — merge main, test, review diff, commit, push, open a PR | Git + GitHub |

### Notes, journaling & planning (need a notes vault)
| Skill | What it does | Needs |
|-------|--------------|-------|
| [daily-process](./daily-process) | Process unfiled notes and surface daily observations | A notes vault (`$VAULT_ROOT`) |
| [weekly-plan](./weekly-plan) | Sunday weekly planning session | A notes vault |
| [monthly-plan](./monthly-plan) | Monthly synthesis + content planning | A notes vault |
| [quarterly-plan](./quarterly-plan) | Quarterly deep review + focus areas for the next 12 weeks | A notes vault |
| [journal-process](./journal-process) | Clean up voice-journal recordings or pasted transcripts | A notes vault |
| [notebooklm](./notebooklm) | Import NotebookLM notebooks into an Obsidian vault as linked knowledge graphs | Obsidian + NotebookLM |

> The planning/notes skills reference a `$VAULT_ROOT` — point it at your own notes folder
> (Obsidian, Logseq, or plain Markdown). No path is hardcoded.

## Using a skill

1. Copy the skill's folder into your agent's skills location (or point your agent at its `SKILL.md`).
2. If the skill has `references/*.example.md`, copy it to the non-`example` name and fill it in.
   Populated config/alias files stay **local** — they're gitignored, never committed.
3. Invoke by describing the task; the agent matches the skill's `description`.

## Conventions

- One folder per skill, kebab-case name matching the `name:` in frontmatter.
- `SKILL.md` is the only required file. `references/` holds templates and supporting docs.
- No hardcoded personal paths, names, or org-internal tooling. Anything machine-specific is a
  `*.example.md` template the user fills in locally.

### Frontmatter schema

Every `SKILL.md` opens with YAML frontmatter using this schema:

| Field | Required | Purpose |
|-------|----------|---------|
| `name` | yes | Kebab-case, matches the folder name |
| `description` | yes | When to use the skill — the text an agent matches against |
| `user-invocable` | no | `true` if the skill is meant to be triggered directly (e.g. as a slash command) |
| `tools` | no | Tool hints for hosts that read them (e.g. `m-skill`). Optional; most skills declare tools in the body instead |

Keep frontmatter to these fields. Setup, adapters, and prose belong in the body.

## License

[MIT](./LICENSE) — use, fork, adapt freely.

## Credits

Some skills are adapted from other open-source projects. See [CREDITS.md](./CREDITS.md) for full
attribution; each derived `SKILL.md` also carries an inline credit footer.
