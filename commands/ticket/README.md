# ingest:ticket

Ticketing command that produces atomic, agent-ready tickets with full specifications from the remediation plan.

## Files

| File | Purpose |
|------|---------|
| `ticket.md` | Main command prompt/skill |
| `ticket-sizing.md` | Story point estimation criteria |
| `ticket-output-template.md` | Template for individual ticket files |
| `dependency-map-template.md` | Template for the dependency map |
| `jira-mapping.md` | Field mapping spec for Jira integration |

## Usage

```
ingest:ticket                              # Generate tickets for full plan
ingest:ticket --workstream           # Tickets for one workstream
ingest:ticket --push jira                  # Push tickets to Jira
ingest:ticket --push ado                   # Push tickets to Azure DevOps
ingest:ticket --dry-run                    # Preview in drafts/ subdirectory
ingest:ticket --template 