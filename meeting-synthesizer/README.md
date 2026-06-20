# MeetingSynthesizer

A portable agent skill that synthesizes a **series of meeting transcripts** into one
hierarchy-weighted, cross-meeting analysis: decisions (with confidence), action items
(with ownership), leadership signals, conflict detection, and theme evolution across sessions.

Single-meeting summaries are the degenerate case. The value is **multi-meeting** analysis —
offsites, planning weeks, recurring series — where the skill finds where session A contradicts
session B, tracks how a position moved over the week, and surfaces what leadership repeated.

## Transcript sources
Source-agnostic. WorkIQ (Microsoft 365 / Teams) is the default adapter; **Zoom** (`.vtt`) and
**Google Meet** (Drive export) transcripts work too, as does plain paste or local files. See the
"Transcript Adapters" section of `SKILL.md`.

## Setup
1. Drop this folder into your agent's skills directory.
2. `cp references/config.example.md references/config.md` and fill in source + output dir + hierarchy.
3. (Optional) `cp references/aliases.example.md references/aliases.md` to map names → tiers for your org.
   **Do not commit a populated `aliases.md`** — it holds real names. It's gitignored.

## Files
- `SKILL.md` — the skill instructions (the only file the agent strictly needs)
- `references/config.example.md` — config template
- `references/aliases.example.md` — alias/hierarchy template (copy → `aliases.md`, keep local)
- `references/output-template.md` — exact output structure
- `.gitignore` — keeps your real config/aliases out of version control

## License
MIT. No hardcoded paths, names, or org-specific tooling. Make it yours.
