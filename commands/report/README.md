# ingest:report

Reporting command that generates human-readable summaries of project health and remediation progress for different audiences.

## Files

| File | Purpose |
|------|---------|
| `report.md` | Main command prompt/skill |
| `summary-report-template.md` | Template for leadership/VP summary report |
| `engineering-report-template.md` | Template for in-depth engineering report |

## Usage

```
ingest:report                              # Default: summary report
ingest:report --format summary             # Leadership/VP summary
ingest:report --format engineering         # In-depth engineering report
ingest:report --scope scan                 # Report on scan results only
ingest:report --scope analysis             # Report on analysis only
ingest:report --scope plan                 # Report on plan only
ingest:report --scope progress             # Report on execution progress only
ingest:report --template 