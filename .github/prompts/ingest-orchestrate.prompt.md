---
description: "Run the full Project Ingest pipeline (or a subset) end-to-end with smart state management."
name: "ingest-orchestrate"
argument-hint: "[--through <stage>] [--from <stage>] [--skip <stage>] [--include-execute] [--gates|--no-gates] [--fresh]"
agent: agent
---

Run the Project Ingest **orchestrate** pipeline.

Default pipeline: `init -> scan -> analyze -> plan -> ticket`. Execute is excluded unless `--include-execute` is specified.

Read and follow the execution flow in [commands/orchestrate/orchestrate.md](../../commands/orchestrate/orchestrate.md).

Reference these supporting files as needed:
- [commands/orchestrate/stage-dependencies.md](../../commands/orchestrate/stage-dependencies.md) — prerequisite and failure rules
- [commands/orchestrate/orchestration-log-template.md](../../commands/orchestrate/orchestration-log-template.md) — run log format

Apply any flags or arguments the user provided: ${input}
