---
description: "Generate atomic, agent-ready tickets from the remediation plan."
name: "ingest-ticket"
argument-hint: "[--workstream <name>] [--push jira|ado] [--dry-run] [--template <path>]"
agent: agent
---

Run the Project Ingest **ticket** stage.

Read and follow the execution flow in [commands/ticket/ticket.md](../../commands/ticket/ticket.md).

Reference these supporting files as needed:
- [commands/ticket/ticket-sizing.md](../../commands/ticket/ticket-sizing.md) — story point estimation criteria
- [commands/ticket/ticket-output-template.md](../../commands/ticket/ticket-output-template.md) — individual ticket format
- [commands/ticket/dependency-map-template.md](../../commands/ticket/dependency-map-template.md) — dependency map format
- [commands/ticket/jira-mapping.md](../../commands/ticket/jira-mapping.md) — Jira field mapping (if pushing)

Template lookup:
1. `.project-ingest/templates/ticket-template.md` (team override)
2. [defaults/ticket-template.md](../../defaults/ticket-template.md) (framework default)

Apply any flags or arguments the user provided: ${input}
