---
description: "Initialize Project Ingest config by auto-detecting repo characteristics and optionally enriching via an interactive quiz."
name: "ingest-init"
argument-hint: "[--force] [--from <org-config>]"
agent: agent
---

Run the Project Ingest **init** stage.

Read and follow the execution flow in [commands/init/init.md](../../commands/init/init.md).

Reference these supporting files as needed:
- [commands/init/detection-rules.md](../../commands/init/detection-rules.md) — what to detect and how
- [commands/init/quiz-flow.md](../../commands/init/quiz-flow.md) — interactive enrichment questions
- [commands/init/templates/config-output.md](../../commands/init/templates/config-output.md) — config file template
- [commands/init/templates/manifest-output.md](../../commands/init/templates/manifest-output.md) — manifest file template
- [commands/init/templates/detection-report-output.md](../../commands/init/templates/detection-report-output.md) — detection report template

Apply any flags or arguments the user provided: ${input}
