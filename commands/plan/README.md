# ingest:plan

Planning command that groups analysis findings into themed workstreams, sequences them by dependencies and severity, and produces an actionable remediation plan.

## Files

| File | Purpose |
|------|---------|
| `plan.md` | Main command prompt/skill |
| `workstream-criteria.md` | How to identify and group workstreams |
| `remediation-plan-template.md` | Template for the overall remediation plan |
| `workstream-template.md` | Template for individual workstream files |

## Usage

```
ingest:plan                              # Generate full remediation plan
ingest:plan --workstream           # Plan a specific workstream only
ingest:plan --interactive                # Collaborate on workstream definition
ingest:plan --autonomous                 # Auto-generate workstreams from analysis
ingest:plan --summary                    # Condensed output
```