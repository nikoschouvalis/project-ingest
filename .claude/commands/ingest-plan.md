# /ingest-plan

Generate remediation plan with themed workstreams from analysis findings.

## Instructions

Read and follow the execution flow in `commands/plan/plan.md`.

Reference these supporting files as needed:
- `commands/plan/workstream-criteria.md` — how to identify and group workstreams
- `commands/plan/remediation-plan-template.md` — overall plan output format
- `commands/plan/workstream-template.md` — individual workstream output format

## Flags

- `--workstream ` — Plan a specific workstream only
- `--interactive` — Collaborate on workstream definition
- `--autonomous` — Auto-generate workstreams
- `--summary` — Condensed output

## Output

- `.project-ingest/plan/remediation-plan.md` — overall plan
- `.project-ingest/plan/workstreams/.md` — per workstream