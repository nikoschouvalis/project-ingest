# Severity Criteria

## Overview

Severity is assigned objectively based on risk and impact. It is NOT influenced by:
- Team priorities (those affect planning, not severity)
- Effort to fix (a Critical issue is Critical even if it's hard to fix)
- How long it's existed (legacy doesn't reduce severity)
- Whether it's "normal" for the industry (common problems are still problems)

---

## Critical

**Core question:** Can this cause harm RIGHT NOW?

**Assign Critical when:**
- Active security vulnerability exploitable without authentication
- Data loss or corruption is possible under normal operation
- Production stability is at risk (crashes, resource exhaustion)
- Sensitive data is actively exposed (secrets in code, PII in logs shipping to third parties)
- Authentication/authorization is fundamentally broken
- A single failure could cascade into system-wide outage

**Examples:**
- Hardcoded production database credentials in committed code
- SQL injection on a public endpoint
- No authentication on admin endpoints
- Missing transaction on financial operations (partial writes possible)
- Infinite loop possible in request handler under certain inputs

**NOT Critical (common mistakes):**
- Outdated dependency with a theoretical CVE (High, not Critical, unless actively exploitable in context)
- Missing tests (High at most — risk is indirect)
- Poor architecture (High at most — impact is velocity, not immediate harm)

---

## High

**Core question:** Will this cause significant pain SOON?

**Assign High when:**
- Security vulnerability that requires specific conditions to exploit
- Reliability issues that will manifest under load or edge cases
- Major velocity blocker (architecture so tangled that changes are dangerous)
- Missing tests on critical paths (changes are risky)
- Performance issues that degrade user experience noticeably
- Operational gaps that will hurt during incidents (no logging, no runbooks)
- Data integrity risks that haven't manifested yet but likely will

**Examples:**
- N+1 queries on a list endpoint that will get slow as data grows
- No integration tests on payment flow
- Circular dependencies making a module impossible to modify safely
- No error tracking — production errors go unnoticed
- Missing rate limiting on authentication endpoints
- No database backups configured

---

## Medium

**Core question:** Is this making things WORSE OVER TIME?

**Assign Medium when:**
- Technical debt that increases cost of future changes
- Inconsistencies that confuse developers and slow onboarding
- Missing documentation that causes repeated questions
- Code quality issues that make bugs more likely over time
- Minor security gaps that are low-risk but should be addressed
- Performance inefficiencies that aren't user-facing yet
- Testing gaps on non-critical paths

**Examples:**
- Duplicated business logic in three places (divergence risk)
- No onboarding documentation (every new dev asks the same questions)
- Inconsistent error handling patterns (some swallow, some throw, some log)
- Missing indexes on queries that are slow but not user-facing
- Dead code that confuses readers
- Outdated dependencies (not vulnerable, just old)

---

## Low

**Core question:** Is this a MISSED OPPORTUNITY?

**Assign Low when:**
- Polish and refinement opportunities
- Minor inconsistencies that don't cause confusion
- Optimization opportunities with minimal impact
- Nice-to-have documentation additions
- Style/pattern preferences where current approach works fine
- Accessibility improvements on non-critical paths

**Examples:**
- Could use a more descriptive variable name
- Missing alt text on a decorative image
- A function could be slightly more efficient but works fine
- README could have a better getting-started section
- Some files don't follow the naming convention but it's not confusing
- A dependency could be replaced with a lighter alternative

---

## Edge Cases

| Scenario | Guidance |
|----------|----------|
| Finding is Critical in one context but Low in another | Assess based on THIS project's context (is it public-facing? handling sensitive data?) |
| Multiple Low findings in same area | Individual findings stay Low, but note the pattern — systemic Low findings may indicate a Medium systemic concern |
| Finding is hard to fix | Severity stays the same. Effort is a planning concern, not a severity concern. |
| Finding is in legacy code being replaced | Still assign severity, but note in root cause that it's in code marked for replacement |
| Finding is in a rarely-used feature | Severity can be lower if blast radius is genuinely small, but don't dismiss just because it's rare |
| Team disagrees with severity | Severity is the framework's objective assessment. Teams can override at the plan stage. |