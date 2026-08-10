# Jira Field Mapping

Field mapping spec used when `ingest:ticket --push jira` pushes generated tickets to Jira.

This maps the fields in `ticket-output-template.md` to Jira issue fields. Teams can override any mapping in `.project-ingest/config.md` under a `jira:` section.

---

## Issue Type

- Default issue type: `Task`
- Tickets grouped under a workstream may be created as `Story` with child `Sub-task`s if the team enables sub-tasks in config.

## Field Mapping

| Ticket Field | Jira Field | Notes |
|--------------|-----------|-------|
| `T-XXX-NNN` (ticket ID) | External ID / labels | Stored as a label `ingest:T-XXX-NNN` for traceability; Jira assigns its own key |
| Title | `summary` | Verb + noun, kept under 255 chars |
| Description + Technical Spec + Constraints | `description` | Rendered as Jira wiki/ADF markup; sections preserved as headings |
| Acceptance Criteria | `description` (Acceptance Criteria heading) or custom field | If team defines `acceptance_criteria_field` in config, mapped there instead |
| Story Points | `customfield_10016` (Story Points) | Field ID configurable via `story_points_field` in config |
| Priority | `priority` | Critical→Highest, High→High, Medium→Medium, Low→Low |
| Workstream | `components` or `labels` | Configurable via `workstream_field`; defaults to a label `ws:<workstream>` |
| Status | `status` | New tickets created in the project's default "To Do" status; `Draft` is not pushed |
| Dependencies (Blocked by / Blocks) | Issue links | `blocks` / `is blocked by` link types |
| References (Finding IDs, files) | `description` (References heading) | Finding IDs added as labels `finding:<id>` |
| Testing Plan | `description` (Testing Plan heading) | Preserved as a checklist |
| Reviewer Checklist | `description` (Reviewer Checklist heading) | Preserved as a checklist |

## Priority Mapping

| Ingest Severity/Priority | Jira Priority |
|--------------------------|---------------|
| Critical | Highest |
| High | High |
| Medium | Medium |
| Low | Low |

## Required Config

To push to Jira, `.project-ingest/config.md` must provide:

- `jira.base_url` — Jira instance URL
- `jira.project_key` — target project key (e.g., `ENG`)
- `jira.auth` — reference to credentials (never store secrets in config; use an env var or secret reference)

Optional overrides:

- `jira.issue_type` (default `Task`)
- `jira.story_points_field` (default `customfield_10016`)
- `jira.acceptance_criteria_field`
- `jira.workstream_field`

## Behavior

- If required config is missing: warn `"Jira push requested but jira config incomplete. Skipping push; tickets written locally."` and continue.
- Dependencies are linked after all tickets are created, so both endpoints exist.
- `--dry-run` never pushes to Jira; it only writes local drafts.
