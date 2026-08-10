# /ingest-orchestrate

Run the full pipeline (or subset) end-to-end with smart state management.

## Instructions

Read and follow the execution flow in `commands/orchestrate/orchestrate.md`.

Reference these supporting files as needed:
- `commands/orchestrate/stage-dependencies.md` — prerequisite and failure rules
- `commands/orchestrate/orchestration-log-template.md` — run log format

## Default Pipeline

init -> scan -> analyze -> plan -> ticket

Execute is excluded unless `--include-execute` is specified.

## Flags

- `--through ` — Stop after specific stage
- `--from ` — Start at specific stage (prerequisites must exist)
- `--skip ` — Skip a stage (with warnings)
- `--include-execute` — Include execution stage
- `--gates` — Pause for approval between stages
- `--no-gates` — Run straight through
- `--fresh` — Re-run all stages regardless of state
- `--interactive` — Global interactive mode
- `--autonomous` — Global autonomous mode
- `--boundary 