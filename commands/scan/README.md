# ingest:scan

Scan command that gathers raw findings across 12 categories by analyzing the codebase holistically.

## Files

| File | Purpose |
|------|---------|
| `scan.md` | Main command prompt/skill |
| `scan-output-template.md` | Template for category scan output |
| `scan-summary-template.md` | Template for full scan summary |
| `categories/arch.md` | Architecture scan instructions |
| `categories/quality.md` | Code Quality scan instructions |
| `categories/security.md` | Security scan instructions |
| `categories/perf.md` | Performance scan instructions |
| `categories/testing.md` | Testing scan instructions |
| `categories/devops.md` | DevOps/CI/CD scan instructions |
| `categories/docs.md` | Documentation scan instructions |
| `categories/deps.md` | Dependencies scan instructions |
| `categories/a11y.md` | Accessibility scan instructions |
| `categories/standards.md` | Standards scan instructions |
| `categories/observe.md` | Observability scan instructions |
| `categories/data.md` | Data scan instructions |

## Usage

```bash
ingest:scan                              # Full scan, all categories, all boundaries
ingest:scan --category security          # Single category
ingest:scan --boundary /apps/web         # Single boundary
ingest:scan --category perf --boundary /apps/web  # Both
ingest:scan --fresh                      # Ignore previous results
ingest:scan --incremental                # Compare against previous, flag resolved
ingest:scan --interactive                # Stop and ask when uncertain
ingest:scan --autonomous                 # Flag uncertain items, continue
ingest:scan --summary                    # Condensed output