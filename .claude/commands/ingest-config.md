# /ingest-config

View, validate, or edit project configuration.

## Instructions

Read and follow the execution flow in `commands/config/config.md`.

Reference these supporting files as needed:
- `commands/config/validation-rules.md` — validation checks

## Flags

- `--show` — Print current config
- `--validate` — Check config for completeness and issues
- `--edit` — Interactive edit session
- `--edit --section ` — Edit a specific section

## Output

- Updated `.project-ingest/config.md` (if edited)
- Validation results (if validating)