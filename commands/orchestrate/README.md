# ingest:orchestrate

Orchestrator agent that runs the full pipeline (or a configured subset) end-to-end, managing state, resumption, and stage coordination.

## Files

| File | Purpose |
|------|---------|
| `orchestrate.md` | Main command prompt/skill |
| `stage-dependencies.md` | Stage prerequisite and failure rules |
| `orchestration-log-template.md` | Template for orchestration run log |

## Usage

```
ingest:orchestrate                                  # Default pipeline: init -> scan -> analyze -> plan -> ticket
ingest:orchestrate --through plan                   # Stop after plan stage
ingest:orchestrate --from analyze                   # Start at analyze (prerequisites must exist)
ingest:orchestrate --from analyze --through plan    # Just analyze and plan
ingest:orchestrate --include-execute                # Include execution stage (changes code)
ingest:orchestrate --gates                          # Pause for approval between stages
ingest:orchestrate --no-gates                       # Run straight through
ingest:orchestrate --fresh                          # Re-run all stages regardless of existing state
ingest:orchestrate --skip                    # Skip a specific stage
ingest:orchestrate --interactive                    # Global interactive mode
ingest:orchestrate --autonomous                     # Global autonomous mode
```