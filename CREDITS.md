# Credits

Several skills in this corpus are adapted from excellent open-source work by others.
All upstreams are MIT-licensed; this repo is also MIT. Where a skill is derived from
an upstream, its `SKILL.md` carries an attribution footer and the original copyright
is acknowledged below.

| Skill(s) | Adapted from | Author | License |
|----------|--------------|--------|---------|
| [`brainstorming`](./brainstorming) | [obra/superpowers](https://github.com/obra/superpowers) — `brainstorming` skill | Jesse Vincent | MIT |
| [`get-api-docs`](./get-api-docs) | [andrewyng/context-hub](https://github.com/andrewyng/context-hub) — `get-api-docs` skill (requires their `chub` CLI) | Context Hub Contributors | MIT |
| [`gstack-browse`](./gstack-browse), [`gstack-qa`](./gstack-qa), [`gstack-ship`](./gstack-ship) | [garrytan/gstack](https://github.com/garrytan/gstack) — `/browse`, `/qa`, `/ship` | Garry Tan | MIT |

## What "adapted" means here

- **`brainstorming`** — forked from superpowers' skill and extended with a premise-challenge
  step, an explicit scope decision (expand / hold / reduce), and a failure-mode check. Host-specific
  skill references (`superpowers:*`) were softened so the skill degrades gracefully on any agent.
- **`get-api-docs`** — closely follows the context-hub skill; it is a thin wrapper over their
  `chub` CLI and is only useful if `chub` is installed.
- **`gstack-*`** — adapted from gstack's slash-command workflows, lightly edited for this corpus's
  conventions (kebab-case folder names, no hardcoded model strings).

All other skills (`causal`, `meeting-synthesizer`, `requirements-builder`, `notebooklm`,
`debugging-vite-apps`, `daily-process`, `weekly-plan`, `monthly-plan`, `quarterly-plan`,
`journal-process`) are original to this repository.

If you believe a skill here derives from your work and isn't credited, please open an issue.
