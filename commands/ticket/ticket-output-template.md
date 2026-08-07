# Ticket Output Template

Template for `.project-ingest/tickets//.md`

---

## Output

```
# [T-XXX-NNN] [Title]

## Metadata
- Workstream: [workstream name]
- Story Points: [1/2/3/5/8/13]
- Priority: [Critical/High/Medium/Low] (inherited from highest-severity finding)
- Status: Draft

## Description

[2-4 sentences: What are we doing and why? Provide enough context for someone unfamiliar with the codebase to understand the purpose. Reference the problem, not just the solution.]

## Acceptance Criteria

- [ ] [Desired end state criterion 1]
- [ ] [Desired end state criterion 2]
- [ ] [Desired end state criterion 3]
- [ ] [Desired end state criterion 4]
- [ ] All new/modified code has test coverage
- [ ] No regressions in existing tests

## Technical Spec

### Approach

[Describe the recommended implementation approach. Be specific enough that an AI agent or developer can start working without asking questions.]

### Files to Modify

| File | What to Look For | What to Do |
|------|-----------------|------------|
| [path/to/file] | [description of current state] | [description of change needed] |
| [path/to/file] | [description of current state] | [description of change needed] |

### Patterns to Follow

[Reference team rulesets or existing patterns in the codebase. Show examples if helpful.]

### Implementation Notes

[Any additional guidance: order of operations, gotchas to watch for, related code to reference as examples.]

## Constraints

[Only include this section if relevant constraints exist. Omit entirely if none.]

- [Do not modify: file/module and why]
- [Must maintain backward compatibility with: what]
- [Performance requirement: must not regress X]
- [Must not break: dependency/integration]

## Testing Plan

### Unit Tests
- [ ] [Test to add/modify]
- [ ] [Test to add/modify]

### Integration Tests
- [ ] [Test to add/modify]

### Manual Verification
- [ ] [Step to verify manually]
- [ ] [Step to verify manually]

### Edge Cases
- [ ] [Edge case to cover]
- [ ] [Edge case to cover]

## Reviewer Checklist

- [ ] [Key thing to verify in PR]
- [ ] [Potential gotcha to check]
- [ ] [Area needing careful review]
- [ ] [Regression concern to validate]

## Dependencies

### Blocked By
- [T-XXX-NNN]: [brief reason why this must complete first]

### Blocks
- [T-XXX-NNN]: [brief reason why this enables that ticket]

(Or "None" if no dependencies)

## Complexity Rationale

**Points:** [n]
**Rationale:** [1-2 sentences explaining why this estimate. What drives the complexity?]

## References

### Source Findings
- [CATEGORY-NNN]: [one-line finding summary]
- [CATEGORY-NNN]: [one-line finding summary]

### Affected Files
- [path/to/file1]
- [path/to/file2]
- [path/to/file3]

### Related Tickets
- [T-XXX-NNN]: [relationship description]

### Related Documentation
- [Link or path to relevant docs, ADRs, or standards]
```