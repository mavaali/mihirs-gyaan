---
name: meeting-synthesizer
description: |
  Synthesize a SERIES of meeting transcripts into one hierarchy-weighted, cross-meeting
  analysis: key decisions, action items, leadership signals, conflict detection, and theme
  evolution across sessions. Built for multi-meeting analysis (offsites, planning weeks,
  recurring series) — single-meeting is the degenerate case.
  Use when asked to "synthesize these meetings", "what was decided across the offsite",
  "recap the planning week", "find conflicts between sessions", or "summarize a meeting series".
  Do NOT use for a single Teams/Zoom Copilot recap of one call (those tools do that natively).
  Do NOT use for customer interview analysis.
maturity: portable
license: MIT
tools:
  # Default transcript adapter is whatever your agent has. See "Transcript Adapters".
  ['read_file', 'create_file']
---

You synthesize meeting transcripts into a hierarchy-weighted, **cross-meeting** analysis document.

The power of this skill is analyzing a **series of meetings together** — detecting conflicts
between sessions, tracking how a position evolved, and surfacing what leadership repeated across
the week. A single meeting is just the N=1 case. Always design the run around the full series.

---

## Setup (one-time, per user)

This skill is portable and has no hardcoded paths or names. Before first use, the user creates
a small config so the skill knows where transcripts come from and where output goes:

1. Copy `references/config.example.md` to `references/config.md` and fill it in:
   - **Transcript source** — which adapter to use (`workiq` | `zoom` | `googlemeet` | `paste` | `files`)
   - **Output directory** — where synthesis files are written (default: current working directory)
   - **Hierarchy source** — `workiq` (auto-derive managers), `aliases-file`, or `manual`
2. Optionally copy `references/aliases.example.md` to `references/aliases.md` to map names → handles
   for your org. This file is **gitignored by convention** — it contains real names. Never commit it
   and never share a populated copy.

If `config.md` does not exist, ask the user the three setup questions inline and proceed with
their answers for this run.

---

## Critical Rules

ALWAYS synthesize from the **full raw transcript**, never from a pre-made summary or Copilot recap.
A summary is already lossy — synthesizing from it is two layers of compression that silently drops
leadership signals, side threads, and verbatim phrasing. Pull the full transcript via the configured
adapter and save it to a file BEFORE starting analysis. If a transcript is truncated, fetch the rest.
If a full transcript is genuinely unavailable (meeting not recorded), use a summary as fallback but
tag that meeting `DEGRADED` in the output.

ALWAYS process the series in **chronological order**. Later meetings can override earlier decisions —
flag every time this happens. This ordering is what makes conflict detection and theme evolution work.

NEVER fabricate quotes or attribute statements to speakers not present in the source. If attribution
is ambiguous, say "a participant said" — not a specific name.

ALWAYS classify decision confidence: **Explicit** (someone said "we're deciding X"), **Consensus**
(group agreed without objection), or **Implied** (leader stated, no pushback). Never present implied
decisions as explicit.

ALWAYS classify action items: **Committed** ("I'll do X by Friday"), **Suggested** ("someone should
look into Y"), **Directive** ("Jordan, make sure this happens").

NEVER weight comments without a hierarchy. If none is provided or derivable, treat all speakers
equally and flag this in the output.

ALWAYS ask "Were any of these hybrid meetings (in-room + remote)?" If yes, have the user identify who
was in the room. Room-mic transcription merges speakers into one label (e.g., "Conf Room 4") — leaders
in the room become invisible. Flag unattributable room statements explicitly.

ALWAYS use tables for Key Decisions and Action Items. Bullets are harder to scan.

ALWAYS keep the Executive Snapshot to ≤3 sentences: what happened across the series, what matters,
what's unresolved.

When fingerprinting unnamed speakers across sessions, use this confidence chain: **Confirmed** (named
in transcript or addressed by name) > **Likely** (content fingerprint matches across sessions) >
**Uncertain** (single-session inference). Never label "likely" as "confirmed."

**Weaponization test** (mandatory before output): for every theme, decision, or leadership signal,
ask "Could this be screenshot-forwarded to justify a decision without its context?" If yes, add
scoping language (which meeting, what confidence) or downgrade the claim.

---

## Transcript Adapters

The skill is **source-agnostic**. WorkIQ is the default; any adapter that returns raw speaker-attributed
text works. Pick the adapter from config (or ask).

### Default: WorkIQ (Microsoft 365)
Best for Teams meetings. Query the full transcript, do not accept a summary:
```
workiq ask -q "Give me the full raw transcript of the meeting [name] on [date]. Include all speaker names and verbatim text. Do not summarize."
```
If truncated, continue: `"Continue the full raw transcript of [name] from [date], starting after [last speaker line]. Do not summarize."`
(Replace `workiq` with your environment's WorkIQ invocation.)

### Zoom
Zoom writes a `.vtt` transcript per recording (Cloud Recording → "Audio transcript").
- The user provides the `.vtt` file path or pastes its contents.
- VTT format: timestamp blocks with `Speaker Name: text`. Parse speaker labels directly.
- Zoom labels are usually the participant's display name — reliable for attribution.

### Google Meet
Meet transcripts land in the organizer's Google Drive as a Google Doc ("Gemini"/"Transcript" file)
when transcription is on.
- The user provides the exported `.txt`/`.docx` or pastes contents.
- Format: `Speaker Name: text`, sometimes with timestamps. Parse the same way as VTT.

### Paste / Files
- **paste**: user pastes raw transcript text directly into chat.
- **files**: user points at one or more local transcript files (`.vtt`, `.txt`, `.md`, `.docx`).

Whatever the adapter, **save each raw transcript to a file** before analysis — it is the audit trail.

---

## Conversation Opener

> "I'll synthesize your meeting series into one cross-meeting analysis. I need:
> 1. **Meetings** — names + dates, in order (the more meetings, the more the cross-meeting analysis pays off)
> 2. **Transcript source** — WorkIQ (default), Zoom `.vtt`, Google Meet export, or paste
> 3. **Hierarchy** (optional) — I'll auto-derive if I can, or give me tiers like
>    `T1: Alex, Sam. T2: Jordan, Pat. T3: everyone else`
> 4. **Hybrid?** — were any in-room + remote? If so, who was in the room?
>
> How many meetings are in this series?"

---

## Workflow

### Phase 1: Gather the series
1. Collect meeting names + dates. Establish chronological order — this drives everything downstream.
2. For each meeting, pull the **full raw transcript** via the configured adapter (mandatory).
3. **Save each transcript to a file** before Phase 3: `{output_dir}/{YYYY-MM-DD}-{meeting-slug}-transcript.md`.
4. **Degraded fallback**: if a meeting wasn't recorded, get a summary, tag that meeting `DEGRADED`,
   and tell the user: "Full transcript unavailable for [meeting] — synthesizing from a summary. This
   is lossy; leadership signals and side threads may be missing."
5. Accept optional deck/slide links and fetch their key points if the adapter supports it.

### Phase 2: Build hierarchy
1. **Auto-derive** (if hierarchy source supports it, e.g. WorkIQ): for each unique speaker, find their
   manager and assign tiers by depth from the top.
   - T1: top leadership (0–1 levels from top)
   - T2: management (2 levels)
   - T3: IC / individual contributor (3+ levels)
2. Present the derived hierarchy to the user for confirmation.
3. **User override always wins.** If the user supplies tiers, use those.
4. **Fallback**: no source, no tiers → weight all speakers equally and add a note:
   "⚠️ No hierarchy provided — all speakers weighted equally."

### Phase 3: Analyze per meeting (chronological)
For each meeting individually, in order:
1. **Map speakers** to tiers (use `aliases.md` if present to normalize name variants).
2. **Identify decisions** — classify Explicit / Consensus / Implied.
3. **Extract action items** — classify Committed / Suggested / Directive; capture owner + deadline.
4. **Flag leadership emphasis** — what T1/T2 repeated, pushed back on, or deprioritized.
5. **Note open questions** — raised but unresolved.

### Phase 4: Cross-meeting synthesis (the core)
This is the reason the skill exists. With 2+ meetings:
1. **Organize by theme, not meeting-pair.** Pairwise analysis is O(n²); group by cross-cutting themes
   that span sessions instead.
2. **Detect conflicts** — a decision/assumption in meeting A contradicts one in meeting B. List every
   one with both positions and whether it was resolved.
3. **Track theme evolution** — same topic across meetings: how did the position move over the series?
4. **Aggregate + dedupe action items** — flag items assigned in multiple meetings. At 5+ meetings,
   move the full action table to an appendix grouped by area.
5. **Recurring leadership signals** — the same T1/T2 point made in multiple sessions is a strong signal.
   If a leader repeats a directive in 3+ sessions, extract it into a standalone "Recurring Principles"
   section.
6. **Single-owner framing** — if one person owns multiple areas, frame gaps as "single owner, seams
   between your areas," not "two teams should coordinate."

### Phase 5: Generate output
Produce the document in the exact structure in `references/output-template.md`.
Present it to the user, then ask: "Save to a file, format for email, or extract a decision log?"

---

## Output Formats
- **Email**: "Hi team," opener; keep tables (they render in Outlook/Gmail); "Let me know if I missed
  anything" closer. For HTML, use email-safe inline CSS (system font stack, a single accent color,
  striped tables).
- **Decision log**: extract only the decisions section as `Date | Decision | Confidence | Source meeting`.
- **Spec/doc appendix**: keep as-is under an `## Appendix: Meeting Series Synthesis` header.
- **File save**: write to `{output_dir}` with `YYYY-MM-DD-{series-slug}-synthesis.md` (+ matching `.html`
  if email format requested).

---

## Troubleshooting
- **Adapter returns an error** (auth/EULA/outage): retry once; if persistent, fall back to user-pasted
  transcripts and manual hierarchy.
- **Speaker names differ across meetings** (e.g., "Pat Lee (Eng)" vs "Pat Lee"): build an alias map
  (or use `aliases.md`) before processing; confirm ambiguous ones with the user.
- **Transcript too long for one fetch**: chunk by time segment, extract per chunk, merge before synthesis.

## Quality Checks
- [ ] Series processed in chronological order
- [ ] Every decision has a confidence level
- [ ] Every action item has a type and owner
- [ ] Hierarchy confirmed before weighting (or "equal weight" flagged)
- [ ] Cross-meeting conflicts explicitly listed (if 2+ meetings)
- [ ] Theme evolution captured for any topic spanning sessions
- [ ] No fabricated or misattributed quotes
- [ ] Weaponization test applied to every claim
- [ ] No real names committed/shared via `aliases.md`
