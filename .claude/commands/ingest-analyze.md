# /ingest-analyze

Analyze scan findings, assign severity, identify root causes and systemic patterns.

## Instructions

Read and follow the execution flow in `commands/analyze/analyze.md`.

Reference these supporting files as needed:
- `commands/analyze/severity-criteria.md` — how to assign severity levels
- `commands/analyze/analysis-output-template.md` — per-category output format
- `commands/analyze/full-analysis-template.md` — cross-category analysis format

## Flags

- `--category ` — Analyze single category
- `--severity ` — Filter output to threshold and above (critical, high, medium, low)
- `--summary` — Condensed output
- `--interactive` — Stop and ask when uncertain
- `--autonomous` — Flag uncertain items, continue

## Output

- `.project-ingest/analysis/-analysis.md` — per category
- `.project-ingest/analysis/full-analysis.md` — cross-category patterns and health