# Performance Scan Instructions

## Category
- ID: `perf`
- Name: Performance
- Finding Prefix: PERF

## Purpose

Identify performance bottlenecks, inefficient patterns, and missing optimizations that impact application speed, resource usage, and user experience.

## Sub-Concerns

### 1. Database & Data Access
- N+1 query patterns (loop that makes a query per iteration)
- Missing indexes (queries filtering/sorting on non-indexed fields)
- Overfetching (SELECT * when only specific fields needed)
- Missing pagination on list endpoints
- Unbounded queries (no LIMIT on potentially large result sets)
- Missing connection pooling
- Redundant queries (same data fetched multiple times in one request)
- Missing eager loading where relationships are always accessed

### 2. Caching
- Missing caching on expensive computations
- Missing caching on frequently-accessed, rarely-changed data
- Missing HTTP caching headers on static/semi-static responses
- Cache invalidation issues (stale data potential)
- Missing memoization on pure functions called repeatedly
- No caching strategy apparent for the application

### 3. Frontend Performance
- Large bundle size (importing entire libraries for single functions)
- Missing code splitting / lazy loading on routes
- Unnecessary re-renders (missing memoization, unstable references)
- Large images without optimization (no lazy loading, no srcset, no compression)
- Blocking resources in critical rendering path
- Missing virtualization for long lists
- Excessive DOM nodes
- Layout thrashing (reading then writing DOM in loops)

### 4. API & Network
- Missing compression (gzip/brotli) on responses
- Chatty APIs (many small requests where one batch would work)
- Missing request deduplication
- No timeout configuration on outbound requests
- Sequential requests that could be parallel
- Large payloads without pagination or streaming
- Missing connection keep-alive

### 5. Memory & Resources
- Memory leaks (event listeners not cleaned up, subscriptions not unsubscribed)
- Unbounded in-memory collections (caches/queues that grow without limit)
- Large objects held in memory unnecessarily
- Missing cleanup in component unmount / process shutdown
- File handles or connections not properly closed

### 6. Algorithms & Logic
- O(n²) or worse algorithms where O(n) or O(n log n) is possible
- Unnecessary iterations (multiple passes where one would suffice)
- Synchronous operations blocking the event loop
- Missing debouncing/throttling on frequent events
- Expensive operations in hot paths (called on every request/render)

## What to Look For

- Database query patterns (ORMs, raw queries, repository methods)
- Loop bodies that make I/O calls
- Import statements (are entire libraries imported?)
- Route handlers — trace the data flow for efficiency
- Component render methods — what triggers re-renders?
- Event handlers — are they cleaned up?
- List rendering — is there virtualization for large lists?
- Image tags — are they optimized?
- API client code — sequential vs. parallel requests

## What to Skip

- Micro-optimizations that don't matter at scale
- Performance in test code
- Build-time performance (unless it's extreme)
- Theoretical performance issues with no evidence of actual impact

## Context to Include

For each finding, note:
- The specific inefficient pattern
- Where it occurs (file, function, route)
- Approximate impact (is this called once at startup or on every request?)
- What the efficient alternative would look like (briefly)