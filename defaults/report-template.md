# Default Report Template

This is the framework's default report template. Teams can override by placing their own at `.project-ingest/templates/report-template.md`.

This default produces a summary-level report suitable for technical leadership.

---

## Template

```
# Project Health Summary

## [Project Name]
Report Date: [date]

---

## Overall Health: [indicator] [label]

[2-3 sentences: Plain-language assessment of project state.]

---

## Key Metrics

| Metric | Value |
|--------|-------|
| Overall Health | [indicator] [label] |
| Critical Issues | [count] |
| High Priority Issues | [count] |
| Total Issues Identified | [count] |
| Workstreams Planned | [count] |
| Estimated Total Effort | [duration] |

---

## Top Risks

1. **[Risk]** — [impact]
2. **[Risk]** — [impact]
3. **[Risk]** — [impact]

---

## Category Overview

| Area | Health | Key Concern |
|------|--------|-------------|
| Security | [indicator] | [summary] |
| Reliability | [indicator] | [summary] |
| Performance | [indicator] | [summary] |
| Maintainability | [indicator] | [summary] |
| Operations | [indicator] | [summary] |

---

## Remediation Plan Summary

| Phase | Focus | Duration | Team |
|-------|-------|----------|------|
| 1 | [workstream] | [duration] | [size] |
| 2 | [workstream] | [duration] | [size] |
| 3 | [workstream] | [duration] | [size] |

---

## Progress

[Current state and progress since last report, if available.]

---

## Recommended Actions

1. [Action]
2. [Action]
3. [Action]

---

## Next Steps

- [Next step]
- [Next step]
```