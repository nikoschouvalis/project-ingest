# Documentation Scan Instructions

## Category
- ID: `docs`
- Name: Documentation
- Finding Prefix: DOCS

## Purpose

Identify gaps, staleness, and quality issues in project documentation that impact onboarding, maintenance, and team effectiveness.

## Sub-Concerns

### 1. Project-Level Documentation
- Missing or minimal README
- No architecture overview / system diagram
- No getting started / onboarding guide
- Missing contribution guidelines
- No explanation of project structure
- README references outdated tools/processes

### 2. API Documentation
- Missing API documentation for public endpoints
- No OpenAPI/Swagger spec (or spec is outdated)
- Missing request/response examples
- Undocumented error responses
- Missing authentication documentation
- No GraphQL schema documentation (if applicable)

### 3. Code Documentation
- Complex functions with no comments explaining "why"
- Public interfaces with no JSDoc/docstrings
- Missing type definitions or unclear types
- Undocumented configuration options
- Missing inline comments on non-obvious logic

### 4. Decision Records
- No ADRs (Architecture Decision Records)
- Major architectural choices with no documented reasoning
- Missing context for "why was it done this way?"
- Outdated ADRs that don't reflect current state

### 5. Operational Documentation
- No runbook for common operations
- Missing incident response documentation
- No monitoring/alerting documentation
- Missing deployment procedures
- No troubleshooting guide

### 6. Staleness & Accuracy
- Documentation that contradicts the code
- References to removed features or deprecated patterns
- Outdated setup instructions
- Broken links in documentation
- Version numbers in docs that don't match current

## What to Look For

- README.md — completeness, accuracy, freshness
- /docs directory — what exists, what's missing
- API route definitions vs. API documentation
- Complex code sections — are they explained?
- Configuration files — are options documented?
- CHANGELOG — does it exist and is it maintained?
- Comments in code — quality and relevance
- Links in documentation — do they work?

## What to Skip

- Documentation style preferences
- Minor typos (unless they cause confusion)
- Auto-generated documentation quality (that's a tooling concern)
- Comments on self-explanatory code

## Context to Include

For each finding, note:
- What's missing or stale
- Who would be impacted (new developers? operators? API consumers?)
- How critical the gap is (is this blocking onboarding or just inconvenient?)
- Whether existing docs exist but are outdated vs. never existed