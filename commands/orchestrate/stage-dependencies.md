# Stage Dependencies & Failure Rules

## Dependency Chain

```
init ──> scan ──> analyze ──> plan ──> ticket ──> execute
```

Each stage requires the previous stage's artifacts to exist.

## Prerequisites Per Stage

| Stage | Required Artifacts | Validated How |
|-------|-------------------|---------------|
| init | None | Always runnable |
| scan | `.project-ingest/config.md` | File exists |
| analyze | `.project-ingest/scans/*.md` (at least one) | Files exist with content |
| plan | `.project-ingest/analysis/full-analysis.md` | File exists with findings |
| ticket | `.project-ingest/plan/remediation-plan.md` | File exists with workstreams |
| execute | `.project-ingest/tickets/**/*.md` (at least one) | Ticket files exist |

## Failure Rules

### Init Failure

**Criticality:** Pipeline-critical
**Behavior:** Abort entire pipeline
**Reason:** Nothing can run without configuration

Possible failures:
- Cannot detect repo root
- User cancels during quiz
- Cannot write config file (permissions)

### Scan Failure

**Criticality:** Pipeline-critical
**Behavior:** Abort entire pipeline
**Reason:** Analysis cannot run without scan data

Possible failures:
- Config references boundaries that don't exist
- Cannot read files in boundary (permissions)
- All categories produce errors

Partial failure handling:
- If some categories succeed and others fail: continue with successful categories
- Log which categories failed and why
- Analysis will only analyze available categories
- Note in orchestration log: "Scan partially complete — [n] categories failed"

### Analyze Failure

**Criticality:** Pipeline-critical
**Behavior:** Abort downstream stages
**Reason:** Plan cannot run without analysis

Possible failures:
- Scan data is malformed or empty
- All categories fail analysis

Partial failure handling:
- If some categories analyze successfully: continue
- Plan will work with available analysis
- Note in orchestration log

### Plan Failure

**Criticality:** Pipeline-critical
**Behavior:** Abort downstream stages
**Reason:** Tickets cannot be generated without a plan

Possible failures:
- Analysis has no findings (nothing to plan)
- Cannot determine workstreams

If analysis has no findings:
- This is actually success — the project is healthy
- Write a plan file noting "no remediation needed"
- Skip ticket stage (nothing to ticket)
- Report success

### Ticket Failure

**Criticality:** Non-critical
**Behavior:** Continue with partial results
**Reason:** Some workstreams may ticket successfully even if others fail

Possible failures:
- Ambiguous findings that can't be decomposed
- Workstream too vague to ticket

Partial failure handling:
- Generate tickets for workstreams that succeed
- Log which workstreams failed
- Flag failed workstreams as "needs human review"
- Continue to execute (if included) with available tickets

### Execute Failure

**Criticality:** Non-critical
**Behavior:** Continue with remaining tickets
**Reason:** Individual ticket failures shouldn't block other tickets

Possible failures:
- Pre-flight check fails
- Agent gets stuck on implementation
- Tests fail after changes
- Guardrail triggered

Partial failure handling:
- Flag failed ticket
- Skip dependent tickets
- Continue with independent tickets
- Report partial completion

## Recovery Guidance

| Failure Type | User Action |
|-------------|-------------|
| Init failure | Fix permissions or re-run interactively |
| Scan partial failure | Check boundary paths, re-run failed categories |
| Analyze failure | Review scan output for malformed data |
| Plan failure (no findings) | Nothing to do — project is healthy |
| Ticket partial failure | Review flagged workstreams, provide clarity, re-run |
| Execute failure | Review execution logs, resolve blockers, re-run ticket |