# Execution Guardrails

## Overview

Guardrails prevent the execution agent from going off-script. They detect when implementation is diverging from the ticket spec and pause for human review.

## File Count Guardrail

### Default Threshold: 10 files

If the agent modifies more than 10 files during a single ticket execution, pause and flag.

### Configuration

Teams can adjust in `.project-ingest/config.md`:
```
## Behavior
- Execution File Threshold: 10
```

### Behavior When Triggered

1. Stop making further changes
2. Do NOT revert changes already made
3. Log current state:
   - Which files have been modified
   - Which files remain to be modified
   - Why more files than expected were needed
4. Flag for human review with message:

```
GUARDRAIL: File count threshold exceeded.
Ticket: T-XXX-NNN
Expected files (from spec): 5
Files modified so far: 11
Threshold: 10

Files modified:
  - src/auth/middleware.ts
  - src/auth/guards.ts
  - src/auth/types.ts
  - ... [full list]

Reason: [agent's explanation of why more files were needed]

Action required: Human review needed.
Options:
  1. Increase threshold and retry
  2. Review changes and approve continuation
  3. Revert and re-scope the ticket
```

### Exceptions

The threshold does NOT count:
- Test files (adding tests is expected to touch many files)
- Type definition files (updating types often cascades)
- Import statement-only changes (adding/removing imports)

The threshold DOES count:
- Source code files with logic changes
- Configuration files
- Migration files

## Scope Drift Guardrail

### What It Detects

The agent is modifying files NOT listed in the ticket's "Files to Modify" section.

### Behavior

- If modifying 1-2 unlisted files: log it, continue (minor drift is normal)
- If modifying 3+ unlisted files: pause and flag

```
GUARDRAIL: Scope drift detected.
Ticket: T-XXX-NNN

Files in ticket spec:
  - src/auth/middleware.ts
  - src/routes/admin.ts

Additional files being modified (not in spec):
  - src/utils/token.ts
  - src/config/auth.ts
  - src/types/auth.ts

Reason: [agent's explanation]

Action required: Human review needed.
```

### Exceptions

Acceptable unlisted file modifications:
- Test files (writing tests for the changes)
- Type/interface files (type updates cascading from changes)
- Import updates in files that import modified modules
- Package manifest updates (adding a dependency)

## No-Touch Guardrail

### What It Detects

The agent is modifying files explicitly listed in the ticket's "Constraints" section as do-not-modify.

### Behavior

- Immediately stop
- Revert the change to that file
- Log the attempt
- Flag for human review

```
GUARDRAIL: Constraint violation.
Ticket: T-XXX-NNN

Constraint: "Do not modify src/legacy/payment-processor.ts"
Attempted: Modification to src/legacy/payment-processor.ts

The agent attempted to modify a file explicitly excluded by ticket constraints.

Action required: Human review needed.
```

## Test Regression Guardrail

### What It Detects

Tests that were passing before execution are now failing.

### Behavior

1. Identify which tests are newly failing
2. Determine if they're related to the changes made
3. If related: attempt to fix (one retry)
4. If unrelated or can't fix: flag

```
GUARDRAIL: Test regression detected.
Ticket: T-XXX-NNN

Previously passing tests now failing:
  - src/auth/auth.test.ts: "should reject expired tokens"
  - src/api/admin.test.ts: "should require auth"

These failures appear to be:
  [x] Related to changes made
  [ ] Unrelated to changes

Attempted fix: [yes/no, what was tried]
Result: [fixed/still failing]

Action required: Human review needed.
```

## Time Guardrail

### What It Detects

Execution of a single ticket is taking excessively long.

### Default Threshold

- 1-2 point tickets: 30 minutes
- 3 point tickets: 45 minutes
- 5 point tickets: 60 minutes
- 8 point tickets: 90 minutes
- 13 point tickets: 120 minutes

### Behavior

When threshold is reached:
- Log current progress
- Flag for human review
- Do NOT automatically abort (agent may be running tests)

```
GUARDRAIL: Time threshold reached.
Ticket: T-XXX-NNN (5 points)
Elapsed: 62 minutes
Threshold: 60 minutes

Current status: [what the agent is doing]
Progress: [what's been completed vs. remaining]

This may indicate the ticket is more complex than estimated.

Action required: Human review — continue or abort?
```

## Guardrail Summary

| Guardrail | Default Threshold | Configurable | Action |
|-----------|------------------|--------------|--------|
| File count | 10 files | Yes | Pause, flag |
| Scope drift | 3+ unlisted files | Yes | Pause, flag |
| No-touch | Any constrained file | No | Stop, revert, flag |
| Test regression | Any new failure | No | Attempt fix, then flag |
| Time | Based on points | Yes | Flag, don't abort |