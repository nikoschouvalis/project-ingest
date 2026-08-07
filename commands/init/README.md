# ingest:init

Setup command that auto-detects repo characteristics and generates project configuration.

## Files

| File | Purpose |
|------|---------|
| `init.md` | Main command prompt/skill |
| `detection-rules.md` | What to look for and how to infer |
| `quiz-flow.md` | Interactive enrichment questions |
| `templates/config-output.md` | Template for generated config |
| `templates/manifest-output.md` | Template for generated manifest |
| `templates/detection-report-output.md` | Template for detection report |

## Usage

```bash
ingest:init                    # Auto-detect, present summary, generate config
ingest:init --force            # Overwrite existing config
ingest:init --from <path>      # Inherit org-level defaults
ingest:init --update           # Re-detect and merge with existing config
ingest:init --edit             # Interactive edit of existing config
ingest:init --skip-quiz        # Auto-detect only, no interactive questions
