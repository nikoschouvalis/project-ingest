# Config Validation Rules

## Overview

Validation checks the config for completeness, consistency, and correctness. Results are categorized as Pass, Warning, or Failure.

## Severity Levels

| Level | Meaning | Action Required |
|-------|---------|-----------------|
| Pass | Correct and complete | None |
| Warning | Missing optional config that would improve results | Recommended but not required |
| Failure | Missing required config or invalid values | Must fix for reliable operation |

## Validation Rules

### Required Fields (Failure if missing)

| Rule | Check | Failure Message |
|------|-------|-----------------|
| Project name | `Project > Name` is not empty | "Project name is required" |
| At least one boundary | `Boundaries` table has at least one row | "At least one boundary must be defined" |
| Boundary path exists | Each boundary path exists on disk | "Boundary [path] does not exist" |
| Boundary has language | Each boundary has a language specified | "Boundary [name] is missing language" |
| Framework version | `Framework > Version` is set | "Framework version is required" |

### Recommended Fields (Warning if missing)

| Rule | Check | Warning Message |
|------|-------|-----------------|
| Ticketing configured | `Tooling > Ticketing` is not "Not configured" | "No ticketing tool configured — ticket push will not work" |
| Priorities set | `Priorities` list exists and has entries | "No priorities configured — using defaults" |
| Behavior mode set | `Behavior > Default Mode` is set | "No default mode set — will prompt each time" |
| Rulesets exist | If rulesets are referenced, files exist at those paths | "Ruleset [path] referenced but file not found" |
| Standards referenced | `Standards` section has at least one entry | "No standards configured — standards scan will be limited" |
| Documentation tool | `Tooling > Documentation` is not "Not configured" | "No documentation tool configured" |

### Consistency Checks (Warning or Failure)

| Rule | Check | Level | Message |
|------|-------|-------|---------|
| Boundary types valid | Type is one of: frontend, backend, library, service, tool | Warning | "Boundary [name] has unrecognized type [type]" |
| No duplicate boundaries | No two boundaries have the same path | Failure | "Duplicate boundary path: [path]" |
| No duplicate names | No two boundaries have the same name | Failure | "Duplicate boundary name: [name]" |
| Template files exist | If custom templates referenced, files exist | Warning | "Template [path] referenced but file not found" |
| Priorities complete | All 12 categories present in priorities list | Warning | "Priorities list is incomplete — missing: [categories]" |
| Valid mode value | Default Mode is "interactive" or "autonomous" | Failure | "Invalid mode: [value]. Must be 'interactive' or 'autonomous'" |
| Valid scan mode | Scan Mode is "fresh" or "incremental" | Failure | "Invalid scan mode: [value]. Must be 'fresh' or 'incremental'" |

### Staleness Checks (Warning)

| Rule | Check | Warning Message |
|------|-------|-----------------|
| Config age | Config was last modified more than 30 days ago | "Config is [n] days old — consider running ingest-init --update" |
| Framework version | Config version doesn't match current framework version | "Config was generated with framework v[old], current is v[new]" |

## Validation Output Format

```
## Validation Results

### Failures ([n])
- [FAIL] [message]
  - Location: [section > field]
  - Current value: [value or "empty"]
  - Required: [what's expected]

### Warnings ([n])
- [WARN] [message]
  - Location: [section > field]
  - Suggestion: [what to do]

### Passed ([n])
- [PASS] [check description]
```