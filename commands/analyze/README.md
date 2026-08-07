# ingest:analyze

Analysis command that interprets scan findings, assigns severity, identifies root causes, and surfaces systemic patterns across the codebase.

## Files

| File | Purpose |
|------|---------|
| `analyze.md` | Main command prompt/skill |
| `severity-criteria.md` | Detailed criteria for assigning severity levels |
| `analysis-output-template.md` | Template for per-category analysis output |
| `full-analysis-template.md` | Template for cross-category full analysis |

## Usage

```bash
ingest:analyze                          # Analyze all scan results
ingest:analyze --category security      # Analyze single category
ingest:analyze --severity high          # Output filtered to High+ only
ingest:analyze --summary                # Condensed output
ingest:analyze --interactive            # Stop and ask when uncertain
ingest:analyze --autonomous             # Flag uncertain items, continue