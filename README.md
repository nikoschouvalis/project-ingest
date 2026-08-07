# Project Ingest

**Version:** 0.1.0

A composable CLI-based framework of Claude commands and skills for analyzing existing codebases, identifying issues, planning remediation, and producing agent-ready tickets.

---

## What Is This?

Project Ingest is a pipeline that takes an existing codebase and systematically:

1. **Sets up** project context and configuration
2. **Scans** for issues across 12 categories
3. **Analyzes** findings with severity and root cause
4. **Plans** remediation into logical workstreams
5. **Tickets** atomic, agent-ready work items with full specs
6. **Executes** via AI agents with human review
7. **Reports** progress to stakeholders
8. **Diffs** runs over time to track improvement

An **orchestrator** can run the full pipeline or any subset end-to-end.

---

## Core Principles

1. **Composable** — Each command does one thing well. Chain them or run independently.
2. **Markdown as interchange** — All artifacts are `.md` files. Human-readable, agent-ingestible, tool-portable.
3. **Flexible with guardrails** — Run anything anytime, but get warnings when prerequisites are missing.
4. **Comprehensive by default** — Full detail always; summaries on request.
5. **Example-driven** — Teams provide templates for tickets, docs, and conventions. Defaults exist for everything.

---

## Quick Reference

| Command | Purpose |
|---------|---------|
| `ingest:init` | Interactive setup quiz, generates config |
| `ingest:config` | View/edit/validate config |
| `ingest:scan` | Gather raw findings by category |
| `ingest:analyze` | Interpret findings, assign severity |
| `ingest:plan` | Group into workstreams, propose remediation |
| `ingest:ticket` | Produce atomic tickets with specs |
| `ingest:execute` | Agent implementation handoff |
| `ingest:report` | Stakeholder-friendly summaries |
| `ingest:diff` | Compare runs over time |
| `ingest:orchestrate` | Run full pipeline or subset |

---

## Global Flags

| Flag | Description |
|------|-------------|
| `--interactive` | Stop and ask when uncertain |
| `--autonomous` | Flag uncertain items as "needs human review" and continue |
| `--summary` | Produce condensed output |
| `--boundary <path>` | Scope to a specific directory/boundary |
| `--category <name>` | Target a specific scan category |

---

## Scan Categories

| ID | Category |
|----|----------|
| `arch` | Architecture |
| `quality` | Code Quality |
| `security` | Security |
| `perf` | Performance |
| `testing` | Testing |
| `devops` | DevOps/CI/CD |
| `docs` | Documentation |
| `deps` | Dependencies |
| `a11y` | Accessibility |
| `standards` | Standards Compliance |
| `observe` | Observability |
| `data` | Data |

---

## Severity Model

| Level | Meaning |
|-------|---------|
| **Critical** | Active risk. Security vulnerability, data loss potential, production instability. |
| **High** | Significant impact on maintainability, reliability, or velocity. Fix soon. |
| **Medium** | Technical debt. Won't break things today, will slow you down over time. |
| **Low** | Nice to have. Polish, minor inconsistencies, optimization opportunities. |

---

## Getting Started

```bash
# Initialize project config (interactive quiz)
ingest:init

# Run a full scan
ingest:scan

# Or scan a specific category on a specific boundary
ingest:scan --category security --boundary /apps/web

# Analyze findings
ingest:analyze

# Generate remediation plan
ingest:plan

# Create tickets
ingest:ticket

# Or run the whole thing
ingest:orchestrate

project-ingest/
├── README.md
├── CHANGELOG.md
├── docs/
│   ├── architecture.md
│   ├── commands.md
│   ├── configuration.md
│   ├── workspace.md
│   ├── severity-model.md
│   ├── session-roadmap.md
│   └── open-questions.md
├── defaults/
│   ├── ticket-template.md
│   ├── report-template.md
│   └── config-template.md
└── commands/
    ├── init/
    ├── scan/
    ├── analyze/
    ├── plan/
    ├── ticket/
    ├── execute/
    ├── report/
    ├── diff/
    └── orchestrate/
    