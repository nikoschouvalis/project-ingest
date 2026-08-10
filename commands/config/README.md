# ingest:config

Configuration management command for viewing, editing, and validating project configuration.

## Files

| File | Purpose |
|------|---------|
| `config.md` | Main command prompt/skill |
| `validation-rules.md` | What validation checks and how |

## Usage

```
ingest-config --show                     # Print current config
ingest-config --validate                 # Check config for completeness and issues
ingest-config --edit                     # Interactive edit session
ingest-config --edit --section     # Edit a specific section
```