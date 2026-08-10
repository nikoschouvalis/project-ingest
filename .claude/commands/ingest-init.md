# /ingest-init

Initialize project configuration by auto-detecting repo characteristics and optionally enriching via interactive quiz.

## Instructions

Read and follow the execution flow in `commands/init/init.md`.

Reference these supporting files as needed:
- `commands/init/detection-rules.md` — what to detect and how
- `commands/init/quiz-flow.md` — interactive enrichment questions
- `commands/init/templates/config-output.md` — config file template
- `commands/init/templates/manifest-output.md` — manifest file template
- `commands/init/templates/detection-report-output.md` — detection report template

## Flags

- `--force` — Overwrite existing config without warning
- `--from 