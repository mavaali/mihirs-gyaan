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
| [`autoresearch-writing`](./autoresearch-writing) | [mavaali/autoresearch-writing](https://github.com/mavaali/autoresearch-writing), itself derived from Karpathy's [autoresearch](https://github.com/karpathy/autoresearch) + Irina Gorbach's article-editing adaptation | Mihir Wagle (loop: Andrej Karpathy; rubric discipline: Irina Gorbach) | MIT |

## What "adapted" means here

- **`brainstorming`** — forked from superpowers' skill and extended with a premise-challenge
  step, an explicit scope decision (expand / hold / reduce), and a failure-mode check. Host-specific
  skill references (`superpowers:*`) were softened so the skill degrades gracefully on any agent.
- **`get-api-docs`** — closely follows the context-hub skill; it is a thin wrapper over their
  `chub` CLI and is only useful if `chub` is installed.
- **`gstack-*`** — adapted from gstack's slash-command workflows, lightly edited for this corpus's
  conventions (kebab-case folder names, no hardcoded model strings).
- **`autoresearch-writing`** — generalized from the upstream's blog-only loop to *any writing*:
  the universal editing loop is separated from a **pluggable, voice-calibrated rubric**, and a
  **chat/file dual mode** was added so it works in a plain chat box or with a file-editing agent.
  The upstream credits Andrej Karpathy's `autoresearch` (one-change-per-experiment, keep-if-it-helps)
  and Irina Gorbach (rubric-scored article editing as isolated hypotheses); those credits carry
  through here. The bundled `rubric.waglesworld-blog.md` is one author's calibration — an example,
  not a default.

All other skills (`causal`, `meeting-synthesizer`, `requirements-builder`, `notebooklm`,
`debugging-vite-apps`, `daily-process`, `weekly-plan`, `monthly-plan`, `quarterly-plan`,
`journal-process`) are original to this repository.

## License notices

The adapted skills derive from these MIT-licensed projects. Their copyright notices are
reproduced here, as the MIT License requires:

- Copyright (c) 2025 Jesse Vincent — [obra/superpowers](https://github.com/obra/superpowers)
- Copyright (c) 2026 Context Hub Contributors — [andrewyng/context-hub](https://github.com/andrewyng/context-hub)
- Copyright (c) 2026 Garry Tan — [garrytan/gstack](https://github.com/garrytan/gstack)
- Copyright (c) 2026 Mihir Wagle — [mavaali/autoresearch-writing](https://github.com/mavaali/autoresearch-writing) (in turn crediting Andrej Karpathy's `autoresearch` and Irina Gorbach)

The MIT permission notice below applies to each of the above:

> Permission is hereby granted, free of charge, to any person obtaining a copy of this software
> and associated documentation files (the "Software"), to deal in the Software without
> restriction, including without limitation the rights to use, copy, modify, merge, publish,
> distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the
> Software is furnished to do so, subject to the following conditions:
>
> The above copyright notice and this permission notice shall be included in all copies or
> substantial portions of the Software.
>
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING
> BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
> NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM,
> DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
> OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

If you believe a skill here derives from your work and isn't credited, please open an issue.
