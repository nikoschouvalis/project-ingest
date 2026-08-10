# Project Ingest Framework — Copilot Instructions

## Context

This repository contains the Project Ingest framework — a composable pipeline for analyzing codebases, identifying issues, planning remediation, and producing agent-ready tickets.

## Commands

When a user invokes a project-ingest command, read the corresponding instruction file:

| Command | Instruction File |
|---------|-----------------|
| /ingest-init | commands/init/init.md |
| /ingest-config | commands/config/config.md |
| /ingest-scan | commands/scan/scan.md |
| /ingest-analyze | commands/analyze/analyze.md |
| /ingest-plan | commands/plan/plan.md |
| /ingest-ticket | commands/ticket/ticket.md |
| /ingest-execute | commands/execute/execute.md |
| /ingest-report | commands/report/report.md |
| /ingest-diff | commands/diff/diff.md |
| /ingest-orchestrate | commands/orchestrate/orchestrate.md |

## How to Execute

1. Read the main command instruction file
2. Read any sub-files it references (categories, templates, criteria)
3. Read the project's `.project-ingest/config.md` if it exists
4. Follow the execution flow defined in the instruction file
5. Write output to the appropriate location in `.project-ingest/`
6. Update `.project-ingest/manifest.md`

## Template Lookup

When a template is needed:
1. Check `.project-ingest/templates/` in the project (team override)
2. Check org config if inherited
3. Use `defaults/` in this framework repo

## Key Rules

- All output is markdown
- Config file is the only hard prerequisite
- Warn on missing prerequisites, don't block
- `--interactive` = stop and ask; `--autonomous` = flag and continue
- Never run execute stage unless explicitly requested
- One ticket = one PR-sized unit of work
- Severity is objective (Critical/High/Medium/Low)
- Findings get unique IDs within their category