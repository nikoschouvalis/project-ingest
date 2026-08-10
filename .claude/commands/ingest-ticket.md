# /ingest-ticket

Generate atomic, agent-ready tickets from the remediation plan.

## Instructions

Read and follow the execution flow in `commands/ticket/ticket.md`.

Reference these supporting files as needed:
- `commands/ticket/ticket-sizing.md` — story point estimation criteria
- `commands/ticket/ticket-output-template.md` — individual ticket format
- `commands/ticket/dependency-map-template.md` — dependency map format
- `commands/ticket/jira-mapping.md` — Jira field mapping (if pushing)

Template lookup:
1. `.project-ingest/templates/ticket-template.md` (team override)
2. `defaults/ticket-template.md` (framework default)

## Flags

- `--workstream ` — Tickets for one workstream
- `--push jira` — Push to Jira
- `--push ado` — Push to Azure DevOps
- `--dry-run` — Preview in drafts/ subdirectory
- `--template 