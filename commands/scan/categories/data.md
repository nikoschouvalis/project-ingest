# Data Scan Instructions

## Category
- ID: `data`
- Name: Data
- Finding Prefix: DATA

## Purpose

Identify issues with data management: schema design, migrations, integrity, and data handling patterns that could lead to corruption, loss, or inconsistency.

## Sub-Concerns

### 1. Schema Design
- Missing indexes on frequently queried fields
- No foreign key constraints where relationships exist
- Inconsistent naming conventions in schema
- Missing NOT NULL constraints on required fields
- Overly permissive column types (text where enum would be appropriate)
- Missing created_at/updated_at timestamps
- No soft delete strategy (if applicable)

### 2. Migrations
- Missing migration files (schema changes made directly)
- Migrations that are not reversible
- Data migrations mixed with schema migrations
- Migration order issues / dependency problems
- Missing migration for recent schema changes
- No migration testing strategy

### 3. Data Integrity
- Missing validation at the data layer (only validated in UI)
- Inconsistent data validation (validated in some paths, not others)
- Race conditions in data access (no optimistic locking, no transactions)
- Missing uniqueness constraints
- Orphaned records possible (no cascade or cleanup)
- Missing data consistency checks

### 4. Data Access Patterns
- Raw queries scattered throughout codebase (no repository/DAO pattern)
- Inconsistent ORM usage (some raw, some ORM in same project)
- Missing transaction boundaries on multi-step operations
- No connection pooling configuration
- Missing retry logic on transient failures
- Unbounded queries (no pagination, no limits)

### 5. Data Safety
- No backup strategy apparent
- Missing data retention policies
- No PII handling documentation
- Missing data encryption at rest
- No audit trail for sensitive data changes
- Missing GDPR/privacy compliance patterns (if applicable)

### 6. Seed & Test Data
- No seed data for development
- No database setup scripts
- Test data that uses production-like PII
- Missing data factories for testing
- No strategy for keeping dev data realistic

## What to Look For

- Migration directories and files
- Schema definitions (SQL files, ORM models, Prisma schema, etc.)
- Database configuration files
- Repository/DAO patterns (or lack thereof)
- Query patterns in route handlers and services
- Transaction usage
- Validation logic location (where is data validated?)
- Backup/retention configuration

## What to Skip

- Database performance tuning (DBA territory)
- Specific query optimization (unless obviously problematic)
- Data warehouse/analytics concerns
- Third-party data service configuration

## Applicability

If no database or data layer is detected, write a minimal scan noting "No data layer detected" with any relevant observations about data handling (e.g., file-based storage, external API reliance).

## Context to Include

For each finding, note:
- Which models/tables/collections are affected
- What the risk is (data loss, corruption, inconsistency, etc.)
- Whether it's a design issue or implementation issue
- How critical the affected data is