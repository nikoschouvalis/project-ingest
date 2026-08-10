# Pre-Flight Checks

## Overview

Pre-flight checks run before any execution begins. ALL must pass for execution to proceed. These protect against creating a mess in an already-messy state.

## Checks

### 1. Clean Git State

**What:** No uncommitted changes, no staged files, no untracked files in working directories.

**How to check:**
- `git status --porcelain` returns empty
- No modified files
- No staged files
- Untracked files in .project-ingest/ are acceptable (we create those)

**Failure message:**
```
FAILED: Working directory is not clean.
Uncommitted changes detected:
  M src/auth/middleware.ts
  ?? src/utils/temp.ts

Action: Commit or stash your changes before running ingest:execute.
```

### 2. Correct Base Branch

**What:** Currently on the expected base branch that PRs will target.

**How to detect base branch:**
1. Check config for explicit base branch setting
2. If not configured: detect default branch (main, master, develop)
3. Use `git remote show origin` or check HEAD reference

**Failure message:**
```
FAILED: Not on base branch.
Current branch: feature/old-work
Expected: main

Action: Switch to your base branch (git checkout main) and retry.
```

### 3. Tests Pass

**What:** Existing test suite passes before we make any changes.

**How to run:**
1. Detect test runner from config or package manifest
2. Run the test command (npm test, pytest, cargo test, etc.)
3. All tests must pass (warnings are acceptable)

**Failure message:**
```
FAILED: Existing tests are failing.
3 tests failed before any changes were made.

Failing tests:
  - src/auth/auth.test.ts: "should validate token"
  - src/api/users.test.ts: "should return 404"
  - src/utils/date.test.ts: "should format correctly"

Action: Fix existing test failures before running ingest:execute.
These failures are not related to ingest changes.
```

### 4. Ticket Exists

**What:** The specified ticket file exists and is parseable.

**How to check:**
- File exists at expected path
- File has required sections (title, description, AC, technical spec)
- File is valid markdown

**Failure message:**
```
FAILED: Ticket not found.
Expected: .project-ingest/tickets/security-hardening/T-SEC-001.md

Action: Run ingest:ticket to generate tickets, or check the ticket ID.
```

### 5. No Branch Conflict

**What:** The branch name we want to create doesn't already exist.

**How to check:**
- Check local branches
- Check remote branches

**Failure message:**
```
FAILED: Branch already exists.
Branch: ingest/T-SEC-001-add-auth-middleware

This ticket may have been previously attempted.
Action: Delete the existing branch or use a different ticket.
Check .project-ingest/execution/ for previous attempt logs.
```

### 6. Dependencies Complete (if applicable)

**What:** If the ticket has "Blocked By" dependencies, those tickets have completed execution.

**How to check:**
- Read ticket's dependencies
- Check for execution logs of blocking tickets
- Verify blocking tickets completed successfully (not flagged)

**Failure message:**
```
FAILED: Unresolved dependencies.
T-SEC-003 is blocked by:
  - T-SEC-001: No execution log found (not yet executed)
  - T-TEST-002: Execution flagged for human intervention

Action: Execute blocking tickets first, or resolve flagged tickets.
```

## Check Order

Run checks in this order (fail fast on cheapest checks first):
1. Ticket exists (file read — instant)
2. No branch conflict (git check — fast)
3. Dependencies complete (file read — fast)
4. Clean git state (git status — fast)
5. Correct base branch (git check — fast)
6. Tests pass (test run — slowest, run last)

## Override

No overrides are available for pre-flight checks. They exist to prevent damage. If a check fails, the underlying issue must be resolved before execution.

Exception: `--dry-run` skips check #3 (tests pass) and #5 (branch conflict) since no changes will be made.