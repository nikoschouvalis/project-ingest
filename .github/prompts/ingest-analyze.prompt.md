---
description: "Analyze scan findings, assign severity, and identify root causes and systemic patterns."
name: "ingest-analyze"
argument-hint: "[--category <name>] [--severity <level>] [--summary] [--interactive|--autonomous]"
agent: agent
---

Run the Project Ingest **analyze** stage.

Read and follow the execution flow in [commands/analyze/analyze.md](../../commands/analyze/analyze.md).

Reference these supporting files as needed:
- [commands/analyze/severity-criteria.md](../../commands/analyze/severity-criteria.md) — how to assign severity levels
- [commands/analyze/analysis-output-template.md](../../commands/analyze/analysis-output-template.md) — per-category output format
- [commands/analyze/full-analysis-template.md](../../commands/analyze/full-analysis-template.md) — cross-category analysis format

Apply any flags or arguments the user provided: ${input}
