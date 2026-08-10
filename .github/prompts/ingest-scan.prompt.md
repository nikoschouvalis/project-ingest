---
description: "Scan the codebase for findings across the 12 Project Ingest categories."
name: "ingest-scan"
argument-hint: "[--category <name>] [--boundary <path>]"
agent: agent
---

Run the Project Ingest **scan** stage.

Read and follow the execution flow in [commands/scan/scan.md](../../commands/scan/scan.md).

Reference these supporting files as needed:
- [commands/scan/scan-output-template.md](../../commands/scan/scan-output-template.md) — output format for category scans
- [commands/scan/scan-summary-template.md](../../commands/scan/scan-summary-template.md) — output format for full scan summary
- Category instructions in [commands/scan/categories/](../../commands/scan/categories/): `arch`, `quality`, `security`, `perf`, `testing`, `devops`, `docs`, `deps`, `a11y`, `standards`, `observe`, `data`.

Apply any flags or arguments the user provided: ${input}
