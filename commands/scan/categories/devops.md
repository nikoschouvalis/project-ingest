# DevOps/CI/CD Scan Instructions

## Category
- ID: `devops`
- Name: DevOps/CI/CD
- Finding Prefix: DEVOPS

## Purpose

Identify gaps in build, deployment, and operational infrastructure that impact reliability, speed of delivery, and environment consistency.

## Sub-Concerns

### 1. CI Pipeline
- Missing CI pipeline entirely
- Tests not running in CI
- Missing linting/formatting checks in CI
- No build verification step
- Missing security scanning in pipeline
- Pipeline doesn't fail on test failures
- Slow pipeline with no optimization (no caching, no parallelization)
- Missing branch protection (can merge without CI passing)

### 2. CD & Deployment
- Manual deployment steps documented but not automated
- No deployment pipeline
- Missing rollback strategy
- No blue/green or canary deployment capability
- Deployment coupled to specific person's machine/credentials
- Missing deployment documentation
- No smoke tests after deployment

### 3. Environment Parity
- Significant differences between dev/staging/production
- Missing local development setup (docker-compose, scripts)
- Environment-specific code paths (if production do X, else do Y)
- Missing environment variable documentation
- Hardcoded environment-specific values
- No staging environment at all

### 4. Infrastructure as Code
- Manual infrastructure changes (no IaC)
- Drift between IaC definitions and actual state
- Missing documentation for infrastructure
- Secrets in IaC files
- No state management for IaC

### 5. Build & Artifacts
- No reproducible builds (missing lock files, unpinned versions)
- Missing build caching
- Large build artifacts (no optimization)
- Missing artifact versioning
- No container image scanning

### 6. Developer Experience
- Missing or broken local development setup
- No seed data or database setup scripts
- Missing contribution guide
- Onboarding requires tribal knowledge
- No hot reload / fast feedback loop configured

## What to Look For

- CI config files (.github/workflows, .gitlab-ci.yml, etc.)
- Dockerfile and docker-compose files
- Deployment scripts or documentation
- Environment files (.env.example, env documentation)
- Makefile, scripts/ directory, package.json scripts
- README sections about setup and deployment
- Branch protection rules (if visible in config)
- Infrastructure directories (terraform/, k8s/, etc.)

## What to Skip

- Specific cloud provider best practices (too specialized)
- Cost optimization (out of scope)
- Detailed Kubernetes configuration review (unless obvious issues)
- Network/firewall configuration

## Context to Include

For each finding, note:
- What's missing or misconfigured
- Impact on team velocity or reliability
- Which environments are affected
- Whether it's a gap (nothing exists) or a problem (exists but broken)