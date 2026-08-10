# Project Ingest Framework

## What This Is

Project Ingest is a composable CLI-based framework for analyzing existing codebases, identifying issues, planning remediation, and producing agent-ready tickets. You are operating within this framework.

## How It Works

The framework is a pipeline of commands, each producing markdown artifacts that the next command consumes:

```
init -> scan -> analyze -> plan -> ticket -> execute
```

Supporting commands: report, diff, orchestrate, config

## Where Things Live

```
commands/              # Command definitions (prompts, instructions, templates)
  init/                # Setup and config generation
  config/              # Config validation and editing
  scan/                # Codebase scanning (12 categories)
  analyze/             # Finding analysis and severity assignment
  plan/                # Workstream planning
  ticket/              # Ticket generation
  execute/             # Agent execution
  report/              # Report generation
  diff/                # Run comparison
  orchestrate/         # Pipeline orchestration
defaults/              # Default templates (used when teams don't provide their own)
docs/                  # Framework documentation
.claude/commands/      # Slash command entry points
```

## Project Workspace

When running against a project, artifacts are stored in `.project-ingest/` within that project:

```
.project-ingest/
  config.md            # Project configuration (required for all commands)
  manifest.md          # Run history and current state
  detection-report.md  # What init auto-detected
  templates/           # Team-provided templates (override defaults)
  rulesets/            # Team-provided standards
  scans/               # Scan output files
  analysis/            # Analysis output files
  plan/                # Remediation plan and workstreams
  tickets/             # Generated tickets
  reports/             # Generated reports
  execution/           # Execution logs
```

## Template Lookup Order

When a command needs a template:
1. Team template: `.project-ingest/templates/.md` (in the project)
2. Org template: referenced via `--from` config inheritance
3. Framework default: `defaults/.md` (in this framework repo)

## Key Principles

1. Each command reads its instruction file from `commands//`
2. Category-specific instructions are in `commands/scan/categories/`
3. All output is markdown files
4. The config file (`.project-ingest/config.md`) is the only hard requirement
5. Commands warn if prerequisites are missing but don't block
6. `--interactive` stops and asks; `--autonomous` flags and continues
7. Execute stage is never run unless explicitly requested

## When Running a Command

1. Read the main command file (e.g., `commands/scan/scan.md`)
2. Read any referenced sub-files (e.g., category instructions)
3. Read the project's `.project-ingest/config.md` for context
4. Read any referenced rulesets from `.project-ingest/rulesets/`
5. Follow the execution flow defined in the command file
6. Write output using the appropriate template
7. Update `.project-ingest/manifest.md`