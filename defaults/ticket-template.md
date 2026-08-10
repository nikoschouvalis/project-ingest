# Default Ticket Template

This is the framework's default ticket template. Teams can override by placing their own template at `.project-ingest/templates/ticket-template.md`.

---

## Template

```
# [TICKET-ID] [Title]

## Metadata
- Workstream: [workstream name]
- Story Points: [1/2/3/5/8/13]
- Priority: [Critical/High/Medium/Low]
- Status: Draft

## Description

[2-4 sentences: What are we doing and why? Provide enough context for someone unfamiliar with the codebase to understand the purpose.]

## Acceptance Criteria

- [ ] [Desired end state criterion 1]
- [ ] [Desired end state criterion 2]
- [ ] [Desired end state criterion 3]
- [ ] All new/modified code has test coverage
- [ ] No regressions in existing tests

## Technical Spec

### Approach
[Describe the recommended implementation approach.]

### Files to Modify
| File | What to Look For | What to Do |
|------|-----------------|------------|
| [path] | [current state] | [change needed] |

### Patterns to Follow
[Reference team rulesets or existing patterns.]

### Implementation Notes
[Additional guidance, order of operations, gotchas.]

## Constraints

[Only if relevant. Omit section if none.]
- [Constraint 1]
- [Constraint 2]

## Testing Plan

### Unit Tests
- [ ] [Test to add/modify]

### Integration Tests
- [ ] [Test to add/modify]

### Manual Verification
- [ ] [Step to verify]

### Edge Cases
- [ ] [Edge case to cover]

## Reviewer Checklist

- [ ] [Key thing to verify]
- [ ] [Potential gotcha]
- [ ] [Regression concern]

## Dependencies

### Blocked By
- [T-XXX-NNN]: [reason] (or "None")

### Blocks
- [T-XXX-NNN]: [reason] (or "None")

## Complexity Rationale

**Points:** [n]
**Rationale:** [1-2 sentences]

## References

### Source Findings
- [CATEGORY-NNN]: [summary]

### Affected Files
- [paths]

### Related Tickets
- [T-XXX-NNN]: [relationship]

### Related Documentation
- [links or paths]
```