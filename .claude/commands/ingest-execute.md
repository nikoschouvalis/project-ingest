# /ingest-execute

Execute tickets by implementing changes, running tests, and creating pull requests.

## Instructions

Read and follow the execution flow in `commands/execute/execute.md`.

Reference these supporting files as needed:
- `commands/execute/preflight-checks.md` — pre-execution validation
- `commands/execute/guardrails.md` — safety thresholds and limits
- `commands/execute/execution-log-template.md` — execution log format

## Flags

- `--ticket ` — Execute a single ticket
- `--workstream ` — Work through workstream respecting dependencies
- `--validate` — Re-check findings after execution
- `--dry-run` — Show what would be done without changes

## Output

- Code changes (branches/PRs)
- `.project-ingest/execution/-log.md` — execution logs

## Safety

This command modifies code. It is excluded from the default orchestration pipeline.
Pre-flight checks must pass before any changes are made.
Guardrails pause execution if scope exceeds expectations.