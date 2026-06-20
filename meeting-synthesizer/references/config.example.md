# MeetingSynthesizer — Config

Copy this file to `config.md` and fill in. `config.md` is read at the start of each run.

## Transcript source
Which adapter to use by default. One of: `workiq` | `zoom` | `googlemeet` | `paste` | `files`

    transcript_source: workiq

- `workiq`     — Microsoft 365 / Teams meetings (default). Pulls full raw transcript via WorkIQ.
- `zoom`       — Zoom Cloud Recording `.vtt` transcript file.
- `googlemeet` — Google Meet transcript exported from Drive (`.txt`/`.docx`).
- `paste`      — User pastes raw transcript text into chat.
- `files`      — User points at local transcript files.

If you use WorkIQ, set the exact command your environment uses to invoke it:

    workiq_command: workiq ask -q "{query}"

## Output directory
Where synthesis + saved transcripts are written. Defaults to the current working directory.

    output_dir: .

## Hierarchy source
How to assign speaker tiers (T1 leadership / T2 management / T3 IC). One of:
`workiq` | `aliases-file` | `manual`

    hierarchy_source: workiq

- `workiq`       — auto-derive each speaker's manager chain via WorkIQ.
- `aliases-file` — read tiers from `aliases.md` (see `aliases.example.md`).
- `manual`       — ask the user for tiers each run.
