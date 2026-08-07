# Workstream Criteria

## What Makes a Good Workstream

A workstream should be:

1. **Themed** — Has a clear, nameable focus that a team can rally around
2. **Bounded** — Has a clear start and end (definition of done)
3. **Coherent** — Findings within it are related and benefit from being addressed together
4. **Right-sized** — Not so small it's trivial, not so large it's overwhelming (S to XL)
5. **Actionable** — A team can pick this up and start working without further decomposition

## Workstream Naming

Names should be:
- Clear and descriptive
- Action-oriented when possible
- Understandable by non-engineers (for stakeholder communication)

Good names:
- Security Hardening
- Test Foundation
- Architecture Decoupling
- API Modernization
- Observability Setup
- Documentation Sprint
- Dependency Modernization
- Performance Optimization
- Data Layer Cleanup
- Frontend Accessibility

Bad names:
- Misc Fixes
- Technical Debt
- Category 3 Issues
- Sprint 4 Work

## Grouping Heuristics

### Group together when:
- Findings share a root cause (fixing the cause resolves multiple findings)
- Findings are in the same files/modules (minimize context switching)
- Fixing one finding makes fixing another easier or safer
- Findings represent different facets of the same problem
- A single engineer/pair could address them all in one focused effort

### Keep separate when:
- Findings require different expertise (frontend vs. backend vs. infra)
- Findings have no dependency relationship
- Combining them would make the workstream too large (XL+)
- They serve different stakeholder concerns (security vs. performance)
- They have different urgency levels that would be obscured by grouping

## Common Workstream Patterns

These are patterns that frequently emerge. Not all will apply to every project.

| Pattern | Typical Contents | When It Appears |
|---------|-----------------|-----------------|
| Security Hardening | SEC findings + auth ARCH + auth TEST + related DEPS | Almost always if security findings exist |
| Test Foundation | TEST findings + test-related DEVOPS + test DOCS | When testing gaps are systemic |
| Architecture Cleanup | ARCH findings + related QUAL + related STD | When coupling/layering issues are significant |
| Observability Setup | OBS findings + logging QUAL + ops DOCS + related DEVOPS | When monitoring is absent/minimal |
| Performance Sprint | PERF findings + related DATA + caching ARCH | When performance issues cluster |
| Documentation Sprint | DOCS findings + related STD + onboarding DEVOPS | When docs are broadly missing |
| Dependency Modernization | DEPS findings + related SEC + related DEVOPS | When deps are significantly outdated |
| Data Layer Cleanup | DATA findings + related PERF + related TEST | When data concerns cluster |
| Accessibility Remediation | A11Y findings + related STD + related TEST | When a11y gaps are significant |
| Developer Experience | DEVOPS findings + DOCS findings + local setup | When onboarding/DX is painful |

## The "General Cleanup" Workstream

Sometimes there are scattered Low/Medium findings that don't fit neatly into a themed workstream. It's acceptable to create a "General Cleanup" or "Code Health" workstream for these, with the following rules:

- It should be the LAST workstream in sequence (lowest priority)
- It should not contain any Critical or High findings (those belong in themed workstreams)
- It should have a clear definition of done (not an endless backlog)
- If it grows too large, split it by boundary or sub-theme

## Consolidation Rules

When you have more than 5 candidate workstreams:

1. Look for workstreams with fewer than 3 findings — can they merge into a related workstream?
2. Look for workstreams that share the same boundary — can they combine?
3. Look for workstreams that would naturally be done by the same person — can they merge?
4. Consider a "General Cleanup" for scattered low-priority items
5. If two workstreams have a dependency relationship AND are both small, consider merging them

When you have fewer than 3 candidate workstreams:

1. This is fine if the analysis only found a focused set of issues
2. Consider splitting if a workstream is XL+ sized
3. Don't create artificial workstreams just to hit a number