# The full map

Every skill in the corpus, by tier, with what it needs and where it sits on the chat → agent
progression. Newest skills land here as rows — the map grows, the structure doesn't.

## Tier 0 — Zero setup (works in any chat box)

Pure instructions. Paste and go. Best place to start.

| Skill | What it does | Lane |
|-------|--------------|------|
| [autoresearch-writing](../../autoresearch-writing) | Scored editing loop — one change per experiment, keep or revert. Chat mode here; file mode with an agent | both (shared first win) |
| [causal](../../causal) | Five-step causal chain before settling on any "why did X happen" | both |
| [brainstorming](../../brainstorming) | Challenge the premise, then design — before you build | coders |
| [requirements-builder](../../requirements-builder) | Feature idea → user stories, acceptance criteria, scope boundaries | coders |
| [meeting-synthesizer](../../meeting-synthesizer) | Cross-meeting synthesis of a transcript series | knowledge |

> `autoresearch-writing` and `meeting-synthesizer` need a little input you supply (a rubric; a
> set of transcripts) but no installed tooling.

## Tier 1 — Needs a notes vault

Set up once via [Track B](./track-b-notes-vault.md). Then:

| Skill | What it does | Needs |
|-------|--------------|-------|
| [daily-process](../../daily-process) | Process unfiled notes, surface observations | `$VAULT_ROOT` |
| [weekly-plan](../../weekly-plan) | Sunday weekly planning session | a vault |
| [monthly-plan](../../monthly-plan) | Monthly synthesis + content planning | a vault |
| [quarterly-plan](../../quarterly-plan) | Quarterly review + focus for the next 12 weeks | a vault |
| [journal-process](../../journal-process) | Clean up voice-journal recordings / transcripts | a vault |
| [notebooklm](../../notebooklm) | Import NotebookLM notebooks as a linked graph | Obsidian + NotebookLM |

## Tier 2 — Needs a CLI agent + a project

Set up once via [Track A](./track-a-cli-agent.md). Then:

| Skill | What it does | Needs |
|-------|--------------|-------|
| [debugging-vite-apps](../../debugging-vite-apps) | Diagnose blank pages, crashes, module errors | a Vite app |
| [get-api-docs](../../get-api-docs) | Fetch authoritative docs before coding against an API | the `chub` CLI |
| [gstack-browse](../../gstack-browse) | QA / dogfooding via browser automation | browser automation |
| [gstack-qa](../../gstack-qa) | Systematically QA a web app, file bugs with evidence | browser automation |
| [gstack-ship](../../gstack-ship) | Ship: merge, test, review, commit, push, open a PR | git + GitHub |

## How to read the progression

- **Start in Tier 0** — feel the difference with zero friction.
- **Add a vault (Track B) or an agent (Track A)** depending on your lane.
- **Tier 1 / Tier 2** unlock once that setup is done.

The same skill can climb tiers: `autoresearch-writing` runs in Tier 0 (chat) and Tier 2
(automated file mode). That's the whole arc in one skill.

← back to [Start Here](./README.md) · do the [exercises](./exercises.md)
