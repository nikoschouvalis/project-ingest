# Testing Scan Instructions

## Category
- ID: `testing`
- Name: Testing
- Finding Prefix: TEST

## Purpose

Identify gaps in test coverage, quality issues in existing tests, and missing test infrastructure that impacts confidence in the codebase.

## Sub-Concerns

### 1. Coverage Gaps
- Critical paths with no tests (auth, payments, data mutations)
- Entire modules/boundaries with no test files
- Public API endpoints with no integration tests
- Complex business logic with no unit tests
- Edge cases not covered (empty inputs, boundary values, error paths)
- Missing negative tests (what should NOT happen)

### 2. Test Quality
- Tests that test implementation details (brittle to refactoring)
- Tests with no meaningful assertions (just "doesn't throw")
- Tests that always pass regardless of code changes
- Overly complex test setup that obscures what's being tested
- Tests that depend on execution order
- Flaky tests (timing-dependent, network-dependent)
- Snapshot tests that are blindly updated without review

### 3. Missing Test Types
- No unit tests (isolated logic testing)
- No integration tests (component interaction)
- No end-to-end tests (full user flows)
- No API contract tests (request/response validation)
- No accessibility tests
- No performance/load tests
- No visual regression tests (if UI-heavy)

### 4. Test Infrastructure
- No test configuration (missing jest.config, pytest.ini, etc.)
- No CI integration (tests don't run automatically)
- No test database/environment setup
- Missing test utilities (factories, fixtures, helpers)
- No mocking strategy (or inconsistent mocking)
- Missing test documentation (how to run, how to write)

### 5. Test Maintenance
- Disabled/skipped tests with no explanation
- Tests for deleted features (testing code that no longer exists)
- Outdated test data/fixtures
- Test files that don't follow naming conventions
- Missing test cleanup (data leaking between tests)

## What to Look For

- Test directories and their contents vs. source directories
- Test file naming patterns (do they match source files?)
- Critical business logic files — do they have corresponding tests?
- Route/endpoint definitions — are they tested?
- Complex conditional logic — are branches covered?
- Error handling code — are error paths tested?
- CI configuration — are tests part of the pipeline?
- Test utilities — are there shared helpers, factories, fixtures?
- package.json/pyproject.toml — test scripts and dependencies

## What to Skip

- Exact coverage percentages (tools measure this better)
- Test style preferences (describe vs. test, etc.)
- Tests for trivial code (simple getters, constants)
- Third-party library testing (not your code)

## Context to Include

For each finding, note:
- What's missing or problematic
- Why it matters (what risk does this gap create?)
- Which files/modules are affected
- Whether it's a pattern (systemic) or isolated