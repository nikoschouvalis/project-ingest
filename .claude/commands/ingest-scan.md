# /ingest-scan

Scan the codebase for findings across 12 categories.

## Instructions

Read and follow the execution flow in `commands/scan/scan.md`.

Reference these supporting files as needed:
- `commands/scan/scan-output-template.md` — output format for category scans
- `commands/scan/scan-summary-template.md` — output format for full scan summary
- `commands/scan/categories/arch.md` — Architecture scan instructions
- `commands/scan/categories/quality.md` — Code Quality scan instructions
- `commands/scan/categories/security.md` — Security scan instructions
- `commands/scan/categories/perf.md` — Performance scan instructions
- `commands/scan/categories/testing.md` — Testing scan instructions
- `commands/scan/categories/devops.md` — DevOps/CI/CD scan instructions
- `commands/scan/categories/docs.md` — Documentation scan instructions
- `commands/scan/categories/deps.md` — Dependencies scan instructions
- `commands/scan/categories/a11y.md` — Accessibility scan instructions
- `commands/scan/categories/standards.md` — Standards scan instructions
- `commands/scan/categories/observe.md` — Observability scan instructions
- `commands/scan/categories/data.md` — Data scan instructions

## Flags

- `--category ` — Scan single category (arch, quality, security, perf, testing, devops, docs, deps, a11y, standards, observe, data)
- `--boundary 