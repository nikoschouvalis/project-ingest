# Code Quality Scan Instructions

## Category
- ID: `quality`
- Name: Code Quality
- Finding Prefix: QUAL

## Purpose

Identify code-level quality concerns: maintainability, readability, complexity, and craftsmanship issues that impact the team's ability to work with the codebase effectively.

## Sub-Concerns

### 1. Dead Code & Unused Artifacts
- Unreachable code paths
- Unused functions, classes, variables, imports
- Commented-out code blocks (significant chunks, not single lines)
- Unused files or modules
- Feature flags that are permanently on/off
- Deprecated code still present with no removal plan

### 2. Duplication
- Copy-pasted logic across files (not DRY)
- Near-duplicate functions with minor variations
- Repeated patterns that should be abstracted
- Duplicated constants or configuration values
- Same validation logic in multiple places

### 3. Complexity
- Functions/methods that are excessively long (50+ lines)
- Deeply nested conditionals (3+ levels)
- Functions with too many parameters (5+)
- Classes/modules with too many responsibilities
- Complex conditional logic that's hard to follow
- Overly clever code that sacrifices readability

### 4. Naming & Readability
- Misleading names (function name doesn't match what it does)
- Inconsistent naming patterns within the same module
- Abbreviations that aren't universally understood
- Generic names that don't convey purpose (data, info, handler, process)
- Boolean variables/functions with unclear polarity

### 5. Error Handling
- Swallowed errors (empty catch blocks)
- Inconsistent error handling patterns
- Missing error handling on operations that can fail
- Overly broad catch blocks (catching all exceptions)
- Error messages that don't help debugging
- Missing error boundaries in UI code

### 6. Code Smells
- Long parameter lists
- Feature envy (method uses another object's data more than its own)
- Data clumps (same group of variables always passed together)
- Primitive obsession (using primitives where value objects would be clearer)
- Inappropriate intimacy between classes/modules
- Refused bequest (inheriting but not using parent behavior)

## What to Look For

- Functions over 50 lines
- Files over 500 lines
- Deeply nested code (3+ levels of indentation in logic)
- Repeated patterns across files
- Empty catch/except blocks
- Variables declared but never used
- Imports that aren't referenced
- Comments that explain "what" instead of "why" (sign of unclear code)

## What to Skip

- Style/formatting issues (linters handle this)
- Single unused imports (auto-fixable, trivial)
- TODO comments (these are intentional markers, not quality issues)
- Test files (different quality standards apply)
- Generated code

## Context to Include

For each finding, note:
- The specific code pattern observed
- How many instances exist (isolated vs. widespread)
- Which files are affected
- Brief explanation of why it impacts maintainability