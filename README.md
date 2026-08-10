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
```

---

## Installing Into a Project

Project Ingest is a set of command definitions that an AI agent (Claude Code or GitHub Copilot) reads and executes. To ingest a project, the framework's command files must be available inside — or alongside — that project's repository. Pick one of the approaches below.

### Option A — Vendor into the target repo (recommended)

Copy the framework's command definitions directly into the project you want to analyze. This keeps everything self-contained and requires no external references.

```bash
# From the root of the project you want to ingest:
cd /path/to/your-project

# Clone the framework somewhere temporary
git clone https://github.com/nikoschouvalis/project-ingest.git /tmp/project-ingest

# Copy the command definitions and defaults into your project
cp -r /tmp/project-ingest/commands        ./commands
cp -r /tmp/project-ingest/defaults        ./defaults

# Copy the agent entry points (choose the ones you use)
cp -r /tmp/project-ingest/.claude         ./.claude      # Claude Code slash commands
mkdir -p ./.github
cp /tmp/project-ingest/.github/copilot-instructions.md ./.github/copilot-instructions.md  # GitHub Copilot instructions
cp -r /tmp/project-ingest/.github/prompts ./.github/prompts   # GitHub Copilot /ingest-* slash commands
```

> **GitHub Copilot slash commands require `.github/prompts/`.** The `/ingest-*` commands only appear in Copilot chat when the `.github/prompts/*.prompt.md` files are present in the target repo. If you clone or pull this framework and the commands don't show up, make sure `.github/prompts/` was copied over.

### Option B — Add as a git submodule

Keep the framework versioned separately and pull updates with `git submodule update --remote`.

```bash
cd /path/to/your-project
git submodule add https://github.com/nikoschouvalis/project-ingest.git .project-ingest-framework
```

With this layout, the command entry points still need to live where the agent looks for them (`.claude/commands/` for Claude Code, `.github/copilot-instructions.md` for Copilot), so symlink or copy those from the submodule:

```bash
mkdir -p .claude .github
ln -s ../.project-ingest-framework/.claude/commands .claude/commands
cp .project-ingest-framework/.github/copilot-instructions.md .github/copilot-instructions.md
cp -r .project-ingest-framework/.github/prompts .github/prompts   # required for Copilot /ingest-* slash commands
```

### Run the pipeline

Once the command files are in place, open the project in your agent and start with `init`, which creates the `.project-ingest/` workspace and configuration:

```bash
ingest:init          # interactive quiz -> writes .project-ingest/config.md
ingest:scan          # gather findings
ingest:analyze       # assign severity and root cause
ingest:plan          # group into workstreams
ingest:ticket        # produce agent-ready tickets
# ...or run everything:
ingest:orchestrate
```

In GitHub Copilot, invoke the same steps with the slash-command form (`/ingest-init`, `/ingest-scan`, ...). These slash commands are defined by the `.github/prompts/*.prompt.md` files, which point at the instruction files under `commands/`. They only appear if `.github/prompts/` exists in the repo, so ensure it was copied in (see above). `.github/copilot-instructions.md` provides the always-on framework context.

### Where artifacts land

All output is written to a `.project-ingest/` directory **inside the target project** — never in the framework repo:

```
your-project/
├── .project-ingest/
│   ├── config.md            # created by ingest:init (required by all commands)
│   ├── manifest.md          # run history and current state
│   ├── scans/               # scan output
│   ├── analysis/            # analysis output
│   ├── plan/                # remediation plan and workstreams
│   ├── tickets/             # generated tickets
│   └── reports/             # generated reports
└── ... your code ...
```

Add `.project-ingest/` to version control if you want run history tracked, or to `.gitignore` if you prefer to keep analysis artifacts local.

---

## Repository Layout

```
project-ingest/
├── README.md
├── CHANGELOG.md
├── .claude/
│   └── commands/            # Claude Code slash-command entry points
├── .github/
│   ├── copilot-instructions.md  # always-on Copilot framework context
│   └── prompts/             # Copilot /ingest-* slash-command wrappers (required)
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
```
