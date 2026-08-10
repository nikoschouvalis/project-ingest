---
description: "Generate a remediation plan with themed workstreams from analysis findings."
name: "ingest-plan"
argument-hint: "[--workstream <name>] [--summary] [--interactive|--autonomous]"
agent: agent
---

Run the Project Ingest **plan** stage.

Read and follow the execution flow in [commands/plan/plan.md](../../commands/plan/plan.md).

Reference these supporting files as needed:
- [commands/plan/workstream-criteria.md](../../commands/plan/workstream-criteria.md) — how to identify and group workstreams
- [commands/plan/remediation-plan-template.md](../../commands/plan/remediation-plan-template.md) — overall plan output format
- [commands/plan/workstream-template.md](../../commands/plan/workstream-template.md) — individual workstream output format

Apply any flags or arguments the user provided: ${input}
