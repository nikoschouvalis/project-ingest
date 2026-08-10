---
description: "Execute tickets by implementing changes, running tests, and creating pull requests. Modifies code — run only when explicitly requested."
name: "ingest-execute"
argument-hint: "[--ticket <id>] [--workstream <name>] [--validate] [--dry-run]"
agent: agent
---

Run the Project Ingest **execute** stage.

> This command modifies code. It is excluded from the default orchestration pipeline.
> Pre-flight checks must pass before any changes are made, and guardrails pause execution if scope exceeds expectations.

Read and follow the execution flow in [commands/execute/execute.md](../../commands/execute/execute.md).

Reference these supporting files as needed:
- [commands/execute/preflight-checks.md](../../commands/execute/preflight-checks.md) — pre-execution validation
- [commands/execute/guardrails.md](../../commands/execute/guardrails.md) — safety thresholds and limits
- [commands/execute/execution-log-template.md](../../commands/execute/execution-log-template.md) — execution log format

Apply any flags or arguments the user provided: ${input}
