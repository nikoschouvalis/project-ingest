# Dependencies Scan Instructions

## Category
- ID: `deps`
- Name: Dependencies
- Finding Prefix: DEPS

## Purpose

Identify risks in the project's dependency tree: outdated packages, known vulnerabilities, license concerns, unused dependencies, and supply chain risks.

## Sub-Concerns

### 1. Outdated Dependencies
- Major version behind (2+ major versions)
- Dependencies with known security patches available
- Frameworks/runtimes approaching end-of-life
- Dependencies that are no longer maintained (archived, abandoned)
- Pinned to very old versions with no documented reason

### 2. Vulnerability Exposure
- Dependencies with known CVEs (check version numbers)
- Transitive dependencies with vulnerabilities
- Dependencies with recent security advisories
- No automated vulnerability scanning configured

### 3. Unused Dependencies
- Packages in manifest but never imported/required
- Dev dependencies that aren't used in any script or config
- Duplicate packages (same functionality, different libraries)
- Dependencies that could be replaced with native/standard library features

### 4. License Risk
- Dependencies with restrictive licenses (GPL in MIT project, etc.)
- Dependencies with no license specified
- License incompatibilities in the dependency tree
- Missing license documentation for the project itself

### 5. Supply Chain
- Dependencies from unknown/untrusted publishers
- Very new dependencies with few downloads/stars (higher risk)
- Dependencies with many maintainers (larger attack surface)
- Missing lock files (non-reproducible installs)
- No integrity checking configured

### 6. Dependency Health
- Overly large dependency tree (too many transitive deps)
- Heavy dependencies used for trivial functionality
- Multiple libraries solving the same problem
- Missing dependency documentation (why was this added?)
- Inconsistent version strategies (some pinned, some floating)

## What to Look For

- Package manifests (package.json, requirements.txt, Cargo.toml, etc.)
- Lock files — do they exist? Are they committed?
- Import/require statements vs. declared dependencies
- Dependency count relative to project complexity
- Last publish dates of key dependencies
- License fields in package metadata
- Duplicate functionality (e.g., both axios and node-fetch)

## What to Skip

- Exact CVE enumeration (dedicated tools do this better)
- Transitive dependency deep analysis (focus on direct deps)
- Dev dependency versions (less critical unless they have vulns)
- Peer dependency warnings (usually noise)

## Context to Include

For each finding, note:
- Which dependency and current version
- What the concern is (outdated, unused, risky license, etc.)
- How critical the dependency is to the project
- Whether alternatives exist