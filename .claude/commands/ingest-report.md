# /ingest-report

Generate human-readable reports of project health and remediation progress.

## Instructions

Read and follow the execution flow in `commands/report/report.md`.

Reference these supporting files as needed:
- `commands/report/summary-report-template.md` — leadership summary format
- `commands/report/engineering-report-template.md` — engineering detail format

Template lookup:
1. `.project-ingest/templates/report-template.md` (team override)
2. `defaults/report-template.md` (framework default)

## Flags

- `--format summary` — Leadership/VP summary (default)
- `--format engineering` — In-depth engineering report
- `--scope ` — Report on specific stage (scan, analysis, plan, progress)
- `--template 