# /ingest-diff

Compare two scan or analysis runs to show what's changed over time.

## Instructions

Read and follow the execution flow in `commands/diff/diff.md`.

Reference these supporting files as needed:
- `commands/diff/diff-output-template.md` — diff report format

## Flags

- `--from ` — Baseline run to compare from
- `--to ` — Target run (default: latest)
- `--category ` — Diff specific category only
- `--raw` — Compare at scan level instead of analysis level

## Output

- `.project-ingest/reports/diff--vs-.md`