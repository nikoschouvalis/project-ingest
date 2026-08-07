# Standards Compliance Scan Instructions

## Category
- ID: `standards`
- Name: Standards Compliance
- Finding Prefix: STD

## Purpose

Identify deviations from the team's defined conventions, patterns, and standards. This category is heavily dependent on team-provided rulesets — without rulesets, it focuses on internal consistency.

## Sub-Concerns

### 1. File & Directory Structure
- Files in wrong directories (based on conventions)
- Inconsistent directory organization across similar modules
- Missing expected directories (no tests next to source, etc.)
- Naming convention violations in file names
- Mixed organizational patterns (some feature-based, some type-based)

### 2. Naming Conventions
- Inconsistent casing (camelCase mixed with snake_case in same context)
- Component naming violations (if conventions defined)
- File naming doesn't match export/class name
- Inconsistent prefixes/suffixes (some services end in Service, others don't)
- Variable/function naming that violates team conventions

### 3. Code Patterns
- Deviations from established patterns (e.g., team uses repository pattern but some modules don't)
- Inconsistent state management approaches
- Mixed async patterns (callbacks, promises, async/await in same codebase)
- Inconsistent error handling patterns
- Deviations from team-defined component patterns

### 4. API Conventions
- Inconsistent endpoint naming (some REST, some not)
- Inconsistent response formats across endpoints
- Mixed authentication patterns
- Inconsistent error response formats
- Missing versioning where team requires it

### 5. Git & Workflow Conventions
- Inconsistent commit message formats
- Missing or inconsistent branch naming
- Large commits that should be broken up (if visible in recent history)
- Missing PR templates or inconsistent PR descriptions

### 6. Configuration Conventions
- Inconsistent environment variable naming
- Configuration in wrong locations
- Missing configuration documentation
- Inconsistent use of config vs. hardcoded values

## Ruleset Dependency

This category's effectiveness depends heavily on team-provided rulesets in `.project-ingest/rulesets/`.

**If rulesets exist:** Scan against them specifically. Each violation is a finding.

**If no rulesets exist:** Focus on internal consistency only:
- Are patterns consistent within the codebase?
- Where does the codebase disagree with itself?
- What appears to be the intended convention vs. where it's violated?

## What to Look For

- Rulesets first — scan against defined standards
- Then internal consistency — where does the code contradict itself?
- File structure patterns — what's the dominant pattern and where does it break?
- Naming patterns — what's the dominant convention and where does it deviate?
- Architectural patterns — what's established and where is it violated?

## What to Skip

- Formatting/style (linters handle this)
- Personal preference issues with no team convention defined
- Legacy code that predates current conventions (note it, but lower confidence)
- Third-party/generated code

## Context to Include

For each finding, note:
- What the convention/standard is (reference ruleset if applicable)
- What the deviation is
- Whether it's an isolated case or a pattern
- Whether it appears to be legacy (predates the convention) or recent