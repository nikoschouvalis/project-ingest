---
description: "Generate human-readable reports of project health and remediation progress."
name: "ingest-report"
argument-hint: "[--format summary|engineering] [--scope <stage>] [--template <path>]"
agent: agent
---

Run the Project Ingest **report** stage.

Read and follow the execution flow in [commands/report/report.md](../../commands/report/report.md).

Reference these supporting files as needed:
- [commands/report/summary-report-template.md](../../commands/report/summary-report-template.md) — leadership summary format
- [commands/report/engineering-report-template.md](../../commands/report/engineering-report-template.md) — engineering detail format

Template lookup:
1. `.project-ingest/templates/report-template.md` (team override)
2. [defaults/report-template.md](../../defaults/report-template.md) (framework default)

Apply any flags or arguments the user provided: ${input}
