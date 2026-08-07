# Ticket Sizing — Story Points

## Overview

Story points estimate relative complexity, not time. They account for:
- Implementation effort
- Uncertainty/risk
- Testing effort
- Review complexity

## Scale

| Points | Meaning | Typical Characteristics |
|--------|---------|------------------------|
| 1 | Trivial | Single file change, obvious fix, minimal testing needed. Config change, copy update, simple rename. |
| 2 | Small | 1-3 files, straightforward approach, clear pattern to follow. Add a test, fix a simple bug, add validation. |
| 3 | Medium | 3-7 files, some decisions to make, moderate testing. New utility function, refactor a module, add an endpoint. |
| 5 | Large | 5-10 files, cross-cutting concern, significant testing. New feature, architectural change to a module, complex refactor. |
| 8 | Very Large | 10+ files, high complexity, significant risk, extensive testing. Cross-boundary changes, new subsystem, major refactor. |
| 13 | Epic-sized | Should probably be split. If it can't be split, it's a major undertaking with high uncertainty. |

## Estimation Guidelines

### Factors that increase points:
- Multiple files/modules affected
- Cross-boundary changes
- Need to maintain backward compatibility
- Complex testing requirements
- High risk of regression
- Uncertainty in approach
- Need for data migration
- External dependencies (APIs, services)

### Factors that decrease points:
- Clear pattern to follow (other code does this already)
- Well-tested area (safety net exists)
- Isolated change (low blast radius)
- Existing utilities/helpers available
- Clear acceptance criteria with no ambiguity

### Common patterns:

| Pattern | Typical Points |
|---------|---------------|
| Add missing test for existing function | 1-2 |
| Fix a hardcoded secret (move to env) | 1-2 |
| Add input validation to an endpoint | 2-3 |
| Add error handling to a module | 2-3 |
| Add logging to a service | 2-3 |
| Refactor a module to extract a concern | 3-5 |
| Add authentication to a set of endpoints | 3-5 |
| Implement caching layer | 5-8 |
| Decouple tightly coupled modules | 5-8 |
| Add integration test suite for a flow | 5-8 |
| Major architectural refactor | 8-13 |
| Database schema migration with data transform | 8-13 |

## When to Split

A ticket should be split when:
- Estimated at 13 points (almost always splittable)
- Estimated at 8 points AND has clearly separable sub-tasks
- Contains both "prep work" and "implementation" (make prep a separate ticket)
- Touches multiple boundaries with independent changes
- Has a "research/spike" component and an "implementation" component

## Rationale Requirement

Every estimate must include a brief rationale:
- What drives the complexity?
- Why this number and not one higher/lower?
- 1-2 sentences is sufficient