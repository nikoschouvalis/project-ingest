# Detection Rules

## Overview

These rules define what the init command looks for when scanning a repository and how to interpret what it finds. Detection should be thorough but fast — read config files and manifests, don't parse every source file.

---

## Languages

### Detection Method
1. Scan file extensions across the repo (sample, don't count every file)
2. Read package manifests for definitive language confirmation
3. Check for language-specific config files

### Evidence Map

| Language | File Extensions | Manifest Files | Config Files |
|----------|----------------|----------------|--------------|
| TypeScript | .ts, .tsx | package.json (has typescript dep) | tsconfig.json |
| JavaScript | .js, .jsx, .mjs, .cjs | package.json | jsconfig.json |
| Python | .py | requirements.txt, setup.py, pyproject.toml, Pipfile | setup.cfg |
| Java | .java | pom.xml, build.gradle | |
| Kotlin | .kt, .kts | build.gradle.kts | |
| Go | .go | go.mod | |
| Rust | .rs | Cargo.toml | |
| Ruby | .rb | Gemfile | .ruby-version |
| C# | .cs | *.csproj, *.sln | |
| PHP | .php | composer.json | |
| Swift | .swift | Package.swift | |
| Dart | .dart | pubspec.yaml | |

---

## Frameworks

### Detection Method
1. Read dependency lists in package manifests
2. Look for framework-specific config files
3. Check import patterns in entry point files

### Evidence Map

| Framework | Package Name | Config Files | Other Evidence |
|-----------|-------------|--------------|----------------|
| React | react | — | JSX/TSX files |
| Next.js | next | next.config.js, next.config.mjs, next.config.ts | /pages or /app directory |
| Vue | vue | vue.config.js, vite.config.ts | .vue files |
| Nuxt | nuxt | nuxt.config.ts | |
| Angular | @angular/core | angular.json | |
| Svelte | svelte | svelte.config.js | .svelte files |
| Express | express | — | app.listen pattern |
| FastAPI | fastapi | — | from fastapi import |
| Django | django | manage.py, settings.py | |
| Flask | flask | — | from flask import |
| Spring Boot | spring-boot-starter | application.properties, application.yml | |
| Rails | rails | Rakefile, config/routes.rb | |
| .NET / ASP.NET | Microsoft.AspNetCore | Program.cs, Startup.cs, appsettings.json | |
| Nest.js | @nestjs/core | nest-cli.json | |
| Laravel | laravel/framework | artisan | |
| Remix | @remix-run/react | remix.config.js | |
| Astro | astro | astro.config.mjs | |

---

## Boundaries

### Detection Method
1. Look for workspace configuration files (monorepo indicators)
2. Analyze top-level directory structure
3. Look for independent package manifests in subdirectories
4. Check for separate build/deploy configurations per directory

### Monorepo Indicators

| Tool | Config File |
|------|-------------|
| pnpm workspaces | pnpm-workspace.yaml |
| npm workspaces | package.json "workspaces" field |
| yarn workspaces | package.json "workspaces" field |
| Lerna | lerna.json |
| Nx | nx.json, workspace.json |
| Turborepo | turbo.json |
| Rush | rush.json |

### Boundary Type Inference

| Signals | Inferred Type |
|---------|---------------|
| UI framework, components, pages, styles | frontend |
| Route handlers, models, migrations, API specs | backend |
| Shared types, utilities, no entry point | library |
| Worker processes, queue consumers, scheduled tasks | service |
| CLI entry point, bin scripts | tool |

### Boundary Naming
- Use the directory name as the boundary name
- If ambiguous, use `<directory>-<type>` (e.g., `web-frontend`)

---

## CI/CD

### Detection Method
Look for CI/CD configuration files in standard locations.

| Tool | File/Directory |
|------|----------------|
| GitHub Actions | .github/workflows/*.yml |
| GitLab CI | .gitlab-ci.yml |
| Jenkins | Jenkinsfile |
| Azure Pipelines | azure-pipelines.yml |
| CircleCI | .circleci/config.yml |
| Travis CI | .travis.yml |
| Bitbucket Pipelines | bitbucket-pipelines.yml |
| AWS CodeBuild | buildspec.yml |
| Google Cloud Build | cloudbuild.yaml |

### What to Extract
- Pipeline names/stages
- Test steps (confirms test runner)
- Deploy steps (confirms deployment strategy)
- Environment references

---

## Test Runners

### Detection Method
1. Look for test configuration files
2. Look for test directories (test/, tests/, __tests__/, spec/)
3. Check CI config for test commands
4. Check package manifest scripts for test commands

| Runner | Config Files | Directories |
|--------|-------------|-------------|
| Jest | jest.config.js/ts, jest.config.json | __tests__/ |
| Vitest | vitest.config.ts | |
| Mocha | .mocharc.yml, .mocharc.js | test/ |
| Pytest | pytest.ini, pyproject.toml [tool.pytest] | tests/ |
| JUnit | — | src/test/ |
| RSpec | .rspec | spec/ |
| Cypress | cypress.config.js/ts | cypress/ |
| Playwright | playwright.config.ts | e2e/, tests/ |
| Testing Library | @testing-library/* in deps | |

---

## Linters & Static Analysis

### Detection Method
Look for configuration files in repo root and boundary roots.

| Tool | Config Files |
|------|-------------|
| ESLint | .eslintrc.*, eslint.config.js |
| Prettier | .prettierrc.*, prettier.config.js |
| Pylint | .pylintrc, pylintrc |
| Black | pyproject.toml [tool.black] |
| Ruff | ruff.toml, pyproject.toml [tool.ruff] |
| RuboCop | .rubocop.yml |
| SonarQube | sonar-project.properties |
| Stylelint | .stylelintrc.* |
| Biome | biome.json |

---

## Documentation

### Detection Method
Look for documentation files and directories.

| Type | Locations |
|------|-----------|
| README | README.md, README.rst, README.txt (root and boundary roots) |
| Docs directory | /docs, /documentation |
| ADRs | /docs/adrs, /docs/adr, /adr |
| API Specs | openapi.yaml, openapi.json, swagger.yaml, swagger.json, schema.graphql |
| Changelog | CHANGELOG.md, CHANGES.md |
| Contributing | CONTRIBUTING.md |
| Wiki references | Links in README to external wiki |
| Storybook | .storybook/ |

---

## Package Managers

### Detection Method
Look for lock files and manifest files.

| Manager | Lock File | Manifest |
|---------|-----------|----------|
| npm | package-lock.json | package.json |
| yarn | yarn.lock | package.json |
| pnpm | pnpm-lock.yaml | package.json |
| pip | — | requirements.txt, requirements/*.txt |
| Poetry | poetry.lock | pyproject.toml |
| Pipenv | Pipfile.lock | Pipfile |
| Cargo | Cargo.lock | Cargo.toml |
| Go modules | go.sum | go.mod |
| Maven | — | pom.xml |
| Gradle | gradle.lockfile | build.gradle, build.gradle.kts |
| Bundler | Gemfile.lock | Gemfile |
| Composer | composer.lock | composer.json |

---

## Containerization & Infrastructure

### Detection Method

| Tool | Files |
|------|-------|
| Docker | Dockerfile, Dockerfile.*, .dockerignore |
| Docker Compose | docker-compose.yml, docker-compose.*.yml, compose.yml |
| Kubernetes | k8s/, kubernetes/, *.k8s.yml, kustomization.yaml |
| Helm | Chart.yaml, /charts |
| Terraform | *.tf, .terraform/ |
| Pulumi | Pulumi.yaml |

---

## Environment Configuration

### Detection Method

| Type | Files |
|------|-------|
| Environment variables | .env, .env.*, env.example, .env.template |
| App config | config/, settings/, application.yml |
| Secrets references | vault references, AWS Secrets Manager refs, .sops.yaml |

---

## Confidence Levels

When reporting detections, assign confidence:

| Confidence | Meaning | Example |
|------------|---------|---------|
| **High** | Config file or manifest explicitly confirms | "react" in package.json dependencies |
| **Medium** | Strong signals but no explicit confirmation | .tsx files exist but no tsconfig.json |
| **Low** | Inferred from indirect evidence | Directory named "api" with Python files |

Report confidence in the detection report. Only include High and Medium confidence items in the generated config by default. Low confidence items go in the detection report as "Uncertain" for user review.