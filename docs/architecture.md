---

# File 2: docs/architecture.md

```markdown
# Architecture & Pipeline

## System Overview

Project Ingest is a composable CLI-based framework of Claude commands and skills. Each command produces markdown artifacts that subsequent commands consume. The pipeline is flexible — commands can be run independently or orchestrated end-to-end.

---

## Pipeline Diagram
---
┌─────────────────────────────────────────────────────────┐
│ PROJECT INGEST │
├─────────────────────────────────────────────────────────┤
│ │
│ ┌──────────┐ ┌──────────┐ ┌──────────┐ │
│ │ SETUP │───▶│ SCAN │───▶│ ANALYZE │ │
│ └──────────┘ └──────────┘ └──────────┘ │
│ │ │
│ ▼ │
│ ┌──────────┐ ┌──────────┐ ┌──────────┐ │
│ │ EXECUTE │◀───│ TICKET │◀───│ PLAN │ │
│ └──────────┘ └──────────┘ └──────────┘ │
│ │
│ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ │
│ ┌──────────┐ ┌──────────┐ ┌──────────────────┐ │
│ │ REPORT │ │ DIFF │ │ ORCHESTRATE │ │
│ └──────────┘ └──────────┘ └──────────────────┘ │
│ │
│ Human-in-the-loop available at every boundary │
│ Each stage produces artifacts consumed by the next │
├─────────────────────────────────────────────────────────┤
│ CONFIG │ AUDIT WORKSPACE │ TEMPLATES │ VERSIONING │
└─────────────────────────────────────────────────────────┘

## Core Principles

### 1. Composable
Each command does one thing well. They can be chained in sequence or run independently. No command assumes the full pipeline has been executed — but it will warn you if prerequisites are missing.

### 2. Markdown as Interchange
All artifacts are `.md` files. This makes them:
- Human-readable (reviewable in any editor, renderable in any tool)
- Agent-ingestible (subsequent commands consume them as context)
- Tool-portable (paste into Jira, Confluence, GitHub, or any documentation platform)

### 3. Flexible with Guardrails
The pipeline has a natural order, but it's not enforced. Run any command at any time. The system will:
- Warn if prerequisites are missing
- Suggest what to run first
- Never block you from proceeding

### 4. Comprehensive by Default
All outputs are detailed and thorough by default. Use `--summary` flags when you need condensed versions. The assumption is that engineers need detail and stakeholders need summaries — both are served.

### 5. Example-Driven
Teams provide their own templates for tickets, reports, and conventions. The framework ships with sensible defaults for everything, but teams are expected to customize. "Here's how we want our tickets to look" is a first-class concept.

---

## Stage Definitions

### Stage 1: SETUP
**Purpose:** Establish project context and configuration.

The setup stage scans the repo to detect languages, frameworks, and structure, then confirms findings with the user via an interactive quiz. The output is a configuration file that all subsequent commands use.

Key decisions made here:
- What are the project boundaries (frontend, backend, shared, etc.)?
- What are the team's priorities?
- What tooling is in use (ticketing, CI/CD, docs)?
- What rulesets/standards apply?

---

### Stage 2: SCAN
**Purpose:** Gather raw findings. Observation, not judgment.

The scan stage walks through the codebase looking for issues across 12 categories. It reports what it finds without assigning severity or recommending fixes. Think of it as the "data gathering" phase.

Key characteristics:
- Can run all categories or a single category
- Can scope to a specific boundary
- Supports fresh (full re-scan) or incremental (detect resolved, find new) modes
- Catches what linters and static analysis tools miss: architecture, patterns, holistic concerns, gaps

---

### Stage 3: ANALYZE
**Purpose:** Interpret scan findings. Assign severity, identify patterns, surface root causes.

The analysis stage takes raw scan data and applies judgment:
- What severity is each finding?
- What's the root cause (vs. symptom)?
- Are there systemic patterns across findings?
- What's the overall health of the project?

Key characteristics:
- Objective, clear, concise, and prioritized
- Critical issues are called out directly
- Cross-category patterns are surfaced (e.g., "lack of testing is enabling security gaps")

---

### Stage 4: PLAN
**Purpose:** Group findings into logical workstreams. Propose remediation approach.

The plan stage takes analyzed findings and organizes them into actionable workstreams:
- What should be fixed together?
- What order makes sense (dependencies, risk, quick wins)?
- What are the logical groupings (security sprint, test foundation, etc.)?

---

### Stage 5: TICKET
**Purpose:** Produce atomic, agent-ready tickets with full specifications.

The ticket stage takes workstreams and breaks them into individual tickets that are:
- Atomic (one concern per ticket)
- Dependency-aware (knows what blocks what)
- Fully specified (description, acceptance criteria, technical spec, testing plan)
- Complexity-estimated
- Ready for an AI agent to pick up and implement without further clarification

---

### Stage 6: EXECUTE
**Purpose:** Hand off to agents for implementation.

The execute stage is the interface between tickets and implementation. Agents pick up tickets, implement changes, and log what was done. Humans review PRs.

Note: This stage defines the interface. Teams may use their own agent execution patterns.

---

### Stage 7: REPORT
**Purpose:** Generate stakeholder-friendly summaries.

Non-technical summaries of project health, progress, and risk for leadership, product owners, and other non-engineering stakeholders.

---

### Stage 8: DIFF
**Purpose:** Compare runs over time.

Track improvement by comparing scan/analysis results across runs. Show what's resolved, what's new, what's regressed.

---

### Stage 9: ORCHESTRATE
**Purpose:** Run the full pipeline (or subset) without manual command chaining.

The orchestrator is an agent that:
- Reads config
- Determines what to run
- Executes stages in sequence
- Respects flags and human-in-the-loop gates
- Produces all artifacts
- Reports completion

---

## Cross-Boundary Findings

When a finding spans multiple boundaries (e.g., API contract mismatch between frontend and backend):
- In `--autonomous` mode: flagged as "needs human review" with both boundaries referenced
- In `--interactive` mode: stops and asks for clarification on ownership and resolution approach

---

## Interaction Modes

| Mode | Behavior |
|------|----------|
| `--interactive` | Stops and asks when encountering uncertainty, ambiguity, or cross-boundary concerns |
| `--autonomous` | Makes best judgment, flags uncertain items as "needs human review", continues |

This flag is respected globally across all commands and by the orchestrator.

---

## Design Decisions

| Decision | Rationale |
|----------|-----------|
| MD over JSON/YAML for artifacts | Readable by humans AND agents. Portable to any tool. |
| No built-in framework rulesets | Teams define their own standards. Framework stays unopinionated. |
| Fresh vs. incremental as a flag | Both have value. Fresh for audits, incremental for progress tracking. |
| Comprehensive by default | Engineers need detail. Summary is opt-in, not the default. |
| Flexible pipeline order | Real projects are messy. Don't force a rigid workflow. |