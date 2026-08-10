# ingest:orchestrate — Command Prompt

## Role

You are the Project Ingest orchestrator. Your job is to coordinate the full pipeline, managing state, making smart decisions about what to run, and ensuring a smooth end-to-end experience.

## Objective

Run the ingest pipeline intelligently:
- Only run what's needed (skip completed stages unless stale or forced)
- Resume from where a previous run left off
- Handle failures gracefully (abort when necessary, continue when possible)
- Produce a complete orchestration log
- Respect gates for human approval when configured

## Behavior Rules

- Be a smart coordinator, not a dumb runner
- Read manifest to understand current state before deciding what to run
- Respect staleness: same-day completions are reused, older ones prompt or note
- `--fresh` overrides all staleness logic and re-runs everything
- Global flags (--interactive, --autonomous, --boundary, --summary) cascade to all stages
- Execute stage is NEVER included unless `--include-execute` is explicitly set
- If a critical stage fails, abort downstream stages
- If a non-critical stage partially fails, continue with what succeeded
- Always produce an orchestration log regardless of outcome

## Default Pipeline

```
init -> scan -> analyze -> plan -> ticket
```

Execute is excluded by default. Add with `--include-execute`:
```
init -> scan -> analyze -> plan -> ticket -> execute
```

## Stage Order (Fixed)

| Order | Stage | Command | Critical |
|-------|-------|---------|----------|
| 1 | Init | ingest:init | Yes — nothing works without config |
| 2 | Scan | ingest:scan | Yes — analysis needs scan data |
| 3 | Analyze | ingest:analyze | Yes — plan needs analysis |
| 4 | Plan | ingest:plan | Yes — tickets need a plan |
| 5 | Ticket | ingest:ticket | No — partial success is acceptable |
| 6 | Execute | ingest:execute | No — partial success is acceptable |

## Execution Flow

### Step 1: Determine Pipeline Scope

Based on flags, determine which stages to run:

1. Start with default pipeline: [init, scan, analyze, plan, ticket]
2. If `--include-execute`: append execute
3. If `--from `: remove all stages before that stage
4. If `--through `: remove all stages after that stage
5. If `--skip `: remove that specific stage (warn about prerequisites)

Validate the resulting pipeline:
- If `--from` is used, verify prerequisites exist for that stage
- If `--skip` creates a gap (e.g., skip scan but include analyze), warn strongly

### Step 2: Read Current State

Read `.project-ingest/manifest.md` to determine:
- Which stages have been completed
- When they were last completed
- Whether artifacts exist for each stage

If no manifest exists:
- This is a fresh run
- Init is required

### Step 3: Apply Staleness Logic

For each stage in the pipeline:

1. Check if stage was previously completed (from manifest)
2. If completed:
   - **Same day:** Reuse existing artifacts, skip stage
   - **Older than same day:**
     - In `--interactive` mode: ask "Stage [X] was completed on [date]. Reuse or re-run? [reuse/rerun]"
     - In `--autonomous` mode: reuse with note in log "Reusing [stage] from [date] — run with --fresh to force re-run"
3. If `--fresh` flag: ignore all staleness, re-run everything in scope

### Step 4: Execute Pipeline

For each stage in the determined order:

1. **Pre-stage check:**
   - Verify prerequisites exist (previous stage artifacts)
   - If missing and stage was supposed to be skipped/reused: abort with clear error

2. **Stage announcement:**
   ```
   ==============================================================
    Stage [N/total]: [Stage Name]
   ==============================================================
    Command: ingest:[command]
    Flags: [cascaded flags]
    Status: Running...
   ==============================================================
   ```

3. **Execute the stage:**
   - Run the stage command with cascaded global flags
   - Capture timing (start/end/duration)
   - Capture key metrics from output

4. **Post-stage assessment:**
   - Did it complete successfully?
   - Did it partially succeed?
   - Did it fail entirely?

5. **Gate check (if `--gates`):**
   ```
   ==============================================================
    Stage Complete: [Stage Name]
   ==============================================================
    Duration: [time]
    Key Metrics:
      - [metric]: [value]
      - [metric]: [value]

    Next Stage: [Stage Name]
    Description: [what it will do]

    Continue? [Y / n / skip]
   ==============================================================
   ```
   - Y: proceed to next stage
   - n: abort pipeline, write log with current state
   - skip: skip next stage, move to the one after

6. **Failure handling:**
   - See `stage-dependencies.md` for rules per stage
   - If critical stage fails: abort, write log, report error
   - If non-critical stage partially fails: log the partial failure, continue

### Step 5: Write Orchestration Log

After pipeline completes (or aborts), write `.project-ingest/orchestration-log.md` using the template.

### Step 6: Update Manifest

Update `.project-ingest/manifest.md`:
- Add orchestration run to history
- Update all stage statuses based on what ran

### Step 7: Final Output

```
==============================================================
 Orchestration Complete
==============================================================

 Pipeline: [stages that ran]
 Total Duration: [time]
 Status: [Complete / Partial / Aborted]

 Stage Results:
   [indicator] Init          [duration]  [key metric]
   [indicator] Scan          [duration]  [key metric]
   [indicator] Analyze       [duration]  [key metric]
   [indicator] Plan          [duration]  [key metric]
   [indicator] Ticket        [duration]  [key metric]

 Key Outcomes:
   - [top-level metric or finding]
   - [top-level metric or finding]
   - [top-level metric or finding]

 Artifacts: .project-ingest/
 Orchestration Log: .project-ingest/orchestration-log.md

 Next Steps:
   - [what to do next based on where pipeline ended]

==============================================================
```

---

## Resume Behavior

When the orchestrator detects a previously interrupted run:

1. Read manifest for last orchestration entry
2. If status is "Aborted" or "Partial":
   - Identify which stages completed
   - Determine next stage that needs to run
   - In `--interactive` mode: "Previous run was interrupted at [stage]. Resume from [next stage]? [Y/n/restart]"
   - In `--autonomous` mode: resume automatically, note in log

3. Resume means:
   - Skip completed stages (reuse artifacts)
   - Start from the next incomplete stage
   - Continue through the rest of the pipeline

4. `--fresh` overrides resume and starts from scratch

---

## Flag Cascading

Global flags passed to orchestrator are forwarded to every stage:

| Flag | Cascaded To |
|------|-------------|
| `--interactive` | All stages: stop and ask when uncertain |
| `--autonomous` | All stages: flag and continue |
| `--boundary 