# ingest:execute

Execution command that picks up tickets, implements changes via AI agent, runs tests, and creates pull requests.

## Files

| File | Purpose |
|------|---------|
| `execute.md` | Main command prompt/skill |
| `preflight-checks.md` | Pre-execution validation rules |
| `guardrails.md` | Safety guardrails and thresholds |
| `execution-log-template.md` | Template for execution logs |

## Usage

```
ingest:execute --ticket              # Execute a single ticket
ingest:execute --workstream        # Work through a workstream respecting dependencies
ingest:execute --validate                # Re-check findings after execution
ingest:execute --dry-run                 # Show what would be done without making changes
```