# Observability Scan Instructions

## Category
- ID: `observe`
- Name: Observability
- Finding Prefix: OBS

## Purpose

Identify gaps in the application's ability to be monitored, debugged, and understood in production. Can you tell what's happening, what went wrong, and why?

## Sub-Concerns

### 1. Logging
- Missing logging on critical operations (auth, payments, data changes)
- Inconsistent log levels (errors logged as info, info logged as debug)
- Missing structured logging (unstructured string concatenation)
- No correlation IDs / request tracing in logs
- Sensitive data in logs (PII, tokens, passwords)
- Missing logging on error paths
- No log aggregation configuration apparent

### 2. Error Tracking
- Unhandled exceptions with no reporting
- Missing global error handlers
- Errors swallowed silently (empty catch blocks)
- No error tracking service integration (Sentry, Datadog, etc.)
- Missing error context (no user ID, no request context in errors)
- Frontend errors not captured

### 3. Metrics & Monitoring
- No application metrics exposed
- Missing health check endpoints
- No performance metrics (response times, throughput)
- Missing business metrics (signups, conversions, etc.)
- No resource utilization tracking
- Missing SLI/SLO definitions

### 4. Distributed Tracing
- No trace context propagation between services
- Missing span creation on key operations
- No tracing library/SDK integrated
- Cross-boundary calls without correlation

### 5. Alerting & Dashboards
- No alerting configuration
- No dashboard definitions
- Missing runbook links in alerts
- No on-call configuration apparent
- Missing SLA/SLO monitoring

### 6. Debugging Support
- No debug mode / verbose logging toggle
- Missing request/response logging capability
- No feature flags for debugging
- Missing audit trail for data changes
- No way to reproduce production issues locally

## What to Look For

- Logging library usage and configuration
- Error handling blocks — do they report somewhere?
- Health check endpoints
- Metrics libraries (prometheus, statsd, etc.)
- Tracing libraries (opentelemetry, jaeger, etc.)
- Error tracking SDKs (Sentry, Bugsnag, etc.)
- Middleware — is there request logging, tracing middleware?
- Configuration for monitoring services
- Alert definitions (if in repo)

## What to Skip

- Specific monitoring tool configuration (too specialized)
- Log storage/rotation (infrastructure concern)
- Network monitoring (infrastructure concern)
- Exact metric naming conventions

## Context to Include

For each finding, note:
- What's missing or insufficient
- Which operations/flows are affected
- Impact on debugging and incident response
- Whether the gap is total (nothing exists) or partial (exists but incomplete)