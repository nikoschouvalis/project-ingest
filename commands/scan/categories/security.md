# Security Scan Instructions

## Category
- ID: `security`
- Name: Security
- Finding Prefix: SEC

## Purpose

Identify security vulnerabilities, risky patterns, and gaps in security posture. Focus on application-level security concerns that static analysis tools often miss — logic flaws, architectural security gaps, and missing protections.

## Sub-Concerns

### 1. Authentication & Authorization
- Missing authentication on routes/endpoints that need it
- Inconsistent auth checks (some routes protected, similar ones not)
- Broken access control (horizontal/vertical privilege escalation paths)
- Hardcoded credentials, API keys, tokens
- Weak password policies or missing password hashing
- Session management issues (no expiry, no rotation, insecure storage)
- Missing CSRF protection on state-changing operations
- JWT implementation issues (no expiry, weak signing, secrets in code)

### 2. Input Validation & Injection
- Missing input validation on user-supplied data
- SQL injection vectors (string concatenation in queries)
- NoSQL injection vectors
- Command injection (user input in shell commands)
- Path traversal vulnerabilities
- XSS vectors (unescaped user content in HTML/templates)
- Template injection
- LDAP injection
- XML external entity (XXE) processing

### 3. Data Exposure
- Sensitive data in logs (passwords, tokens, PII)
- Sensitive data in error messages returned to clients
- Overly permissive API responses (returning more data than needed)
- Sensitive data in URL parameters (visible in logs, history)
- Missing data masking/redaction
- PII stored without encryption
- Sensitive data in client-side storage (localStorage, cookies without flags)

### 4. Configuration & Secrets
- Secrets in source code (API keys, passwords, connection strings)
- Secrets in config files that are committed
- Missing security headers (CORS, CSP, HSTS, X-Frame-Options)
- Debug mode enabled in production configs
- Default credentials not changed
- Overly permissive CORS configuration
- Missing rate limiting configuration

### 5. Dependency & Supply Chain
- Known vulnerable dependencies (check version numbers against known CVEs)
- Dependencies from untrusted sources
- Missing integrity checks (no lock files, no checksum verification)
- Overly broad dependency permissions
- Post-install scripts in dependencies

### 6. Cryptography
- Weak hashing algorithms (MD5, SHA1 for security purposes)
- Hardcoded encryption keys
- Missing encryption for sensitive data at rest
- Insecure random number generation for security purposes
- Custom crypto implementations (instead of using libraries)

## What to Look For

- Route/endpoint definitions — check for auth middleware
- Database queries — check for parameterization
- User input handling — trace from input to usage
- Config files — look for secrets, debug flags
- .env files — check if .env.example exposes structure
- API responses — check what data is returned
- Error handlers — check what's exposed in errors
- Logging statements — check for sensitive data
- File upload handling — check for validation
- Redirect logic — check for open redirects

## What to Skip

- Dependency vulnerability scanning (tools like Snyk/Dependabot handle this better)
- Network-level security (firewalls, TLS config — infrastructure concern)
- Penetration testing scenarios (this is code review, not pen testing)
- Test credentials in test files (these are expected)

## Context to Include

For each finding, note:
- The specific vulnerability pattern
- Where user input enters and where it's used unsafely
- What an attacker could potentially do (brief threat description)
- Whether it's in a route that's publicly accessible vs. internal