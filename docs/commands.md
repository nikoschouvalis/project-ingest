# Command Reference

## Global Flags

These flags are available on all commands:

| Flag | Description | Default |
|------|-------------|---------|
| `--interactive` | Stop and ask when uncertain | Per config |
| `--autonomous` | Flag uncertain items, continue | Per config |
| `--summary` | Produce condensed output | Off (comprehensive) |
| `--boundary <path>` | Scope to a specific directory | All boundaries |
| `--verbose` | Extra logging/debug output | Off |

---

## ingest:init

**Purpose:** Interactive setup quiz that scans the repo, detects project characteristics, and generates configuration.

| Flag | Description |
|------|-------------|
| `--force` | Overwrite existing config |
| `--from <path>` | Inherit from an org-level config file |

**Prerequisites:** None (this is always the starting point)

**Produces:**
- `.project-ingest/config.md`
- `.project-ingest/manifest.md`

**Behavior:**
1. Scans repo for languages, frameworks, file structure
2. Detects existing tooling (test runners, CI config, linters)
3. Asks confirming questions (8-12 max)
4. Generates config file
5. Creates workspace directory structure

---

## ingest:config

**Purpose:** View, edit, or validate existing configuration.

| Flag | Description |
|------|-------------|
| `--validate` | Check config for completeness and consistency |
| `--show` | Print current config |
| `--edit` | Interactive edit mode |

**Prerequisites:** `ingest:init` (config must exist)

**Produces:**
- Updated `.project-ingest/config.md` (if edited)

---

## ingest:scan

**Purpose:** Gather raw findings by category. Observation, not judgment.

| Flag | Description |
|------|-------------|
| `--category <name>` | Scan a single category |
| `--boundary <path>` | Scope to a specific boundary |
| `--fresh` | Full re-scan, ignore previous results |
| `--incremental` | Detect resolved items, scan for new |
| `--interactive` | Stop and ask when uncertain |
| `--autonomous` | Flag uncertain items, continue |

**Prerequisites:** `.project-ingest/config.md` must exist (warns if missing)

**Produces:**
- `.project-ingest/scans/<category>-scan.md` — Per category
- `.project-ingest/scans/full-scan-summary.md` — When running all categories

**Categories:**

| ID | Category | What It Looks For |
|----|----------|-------------------|
| `arch` | Architecture | Coupling, layering violations, circular dependencies, separation of concerns, module boundaries |
| `quality` | Code Quality | Dead code, duplication, complexity hotspots, naming inconsistencies, code smells |
| `security` | Security | Hardcoded secrets, injection vectors, auth/authz gaps, data exposure, OWASP concerns |
| `perf` | Performance | N+1 queries, missing caching, bundle size, memory leaks, unnecessary re-renders |
| `testing` | Testing | Coverage gaps, missing test types (unit/integration/e2e), brittle tests, test quality |
| `devops` | DevOps/CI/CD | Pipeline gaps, environment parity, manual deployment steps, missing automation |
| `docs` | Documentation | Missing/stale docs, no API specs, no onboarding guide, undocumented decisions |
| `deps` | Dependencies | Outdated packages, known vulnerabilities, license risk, unused dependencies |
| `a11y` | Accessibility | WCAG violations, missing ARIA labels, keyboard navigation gaps, screen reader issues |
| `standards` | Standards | Org convention violations, file structure inconsistencies, pattern deviations |
| `observe` | Observability | Missing logging, no distributed tracing, no alerting, insufficient monitoring |
| `data` | Data | Schema issues, migration gaps, data integrity concerns, missing seed data |

---

## ingest:analyze

**Purpose:** Interpret scan findings. Assign severity, identify patterns, surface root causes.

| Flag | Description |
|------|-------------|
| `--category <name>` | Analyze a single category |
| `--severity <level>` | Filter to specific severity threshold and above |
| `--summary` | Condensed analysis |

**Prerequisites:** Scan results must exist for the targeted categories (warns if missing)

**Produces:**
- `.project-ingest/analysis/<category>-analysis.md` — Per category
- `.project-ingest/analysis/full-analysis.md` — Cross-category patterns, systemic issues, health assessment

**Severity Model:**

| Level | Definition | Action |
|-------|-----------|--------|
| **Critical** | Active risk. Security vulnerability, data loss potential, production instability. | Immediate attention required |
| **High** | Significant impact on maintainability, reliability, or velocity. | Fix soon, plan within current cycle |
| **Medium** | Technical debt. Won't break today, slows you down over time. | Plan for upcoming cycles |
| **Low** | Nice to have. Polish, minor inconsistencies, optimization. | Backlog, address opportunistically |

---

## ingest:plan

**Purpose:** Group findings into logical workstreams. Propose remediation approach and sequencing.

| Flag | Description |
|------|-------------|
| `--workstream <name>` | Plan a specific workstream only |
| `--interactive` | Collaborate on workstream definition |
| `--autonomous` | Auto-generate workstreams from analysis |

**Prerequisites:** Analysis results must exist (warns if missing)

**Produces:**
- `.project-ingest/plan/remediation-plan.md` — Overview of all workstreams, sequencing, dependencies
- `.project-ingest/plan/workstreams/<name>.md` — Detailed plan per workstream

**Workstream examples:**
- Security Hardening
- Test Foundation
- Architecture Cleanup
- Documentation Sprint
- Dependency Modernization
- Performance Optimization
- Observability Setup

---

## ingest:ticket

**Purpose:** Produce atomic, agent-ready tickets with full specifications.

| Flag | Description |
|------|-------------|
| `--workstream <name>` | Generate tickets for one workstream |
| `--push jira` | Push tickets to Jira |
| `--push ado` | Push tickets to Azure DevOps |
| `--dry-run` | Preview tickets without pushing |
| `--template <path>` | Use a team-provided ticket template |
| `--complexity-only` | Just estimate complexity, don't write full specs |
| `--interactive` | Pause for clarification on ambiguous tickets |
| `--autonomous` | Flag ambiguous tickets as "needs human review" |

**Prerequisites:** Remediation plan must exist (warns if missing)

**Produces:**
- `.project-ingest/tickets/<workstream>/<ticket-id>.md` — Individual ticket files
- `.project-ingest/tickets/dependency-map.md` — Cross-ticket dependency graph

**Default Ticket Structure:**
[TICKET-ID] Title

Description

What and why.

Acceptance Criteria

[ ] Criterion 1
[ ] Criterion 2
Technical Spec

How to approach. Files affected. Patterns to follow.

Testing Plan

What to test. How to verify.

Dependencies

Blocked by: [TICKET-X]
Blocks: [TICKET-Y]
Complexity

Estimate: S / M / L / XL

References

Analysis: link to finding
Files: list of affected paths

---

## ingest:execute

**Purpose:** Hand off tickets to agents for implementation.

| Flag | Description |
|------|-------------|
| `--ticket ` | Execute a single ticket |
| `--workstream ` | Work through a workstream respecting dependencies |
| `--validate` | Re-scan to verify fixes after execution |
| `--dry-run` | Show what would be done without making changes |

**Prerequisites:** Tickets must exist for the targeted scope (warns if missing)

**Produces:**
- Code changes (branches/PRs)
- `.project-ingest/execution/-log.md` — What was done, decisions made, files changed

---

## ingest:report

**Purpose:** Generate stakeholder-friendly, non-technical summaries.

| Flag | Description |
|------|-------------|
| `--format ` | Output format: `summary`, `detailed`, `executive` |
| `--scope ` | Report on a specific stage (scan, analysis, plan, progress) |
| `--template 