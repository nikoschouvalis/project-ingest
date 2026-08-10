# ingest:diff

Diff command that compares two scan or analysis runs to show what's changed: resolved findings, new findings, and regressions.

## Files

| File | Purpose |
|------|---------|
| `diff.md` | Main command prompt/skill |
| `diff-output-template.md` | Template for diff report |

## Usage

```
ingest:diff                                # Compare latest vs. previous run
ingest:diff --from           # Specify baseline
ingest:diff --to             # Specify target (default: latest)
ingest:diff --category               # Diff a specific category only
ingest:diff --raw                          # Compare at scan level (not analysis)
```