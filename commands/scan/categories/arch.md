# Architecture Scan Instructions

## Category
- ID: `arch`
- Name: Architecture
- Finding Prefix: ARCH

## Purpose

Identify structural and architectural concerns: how the system is organized, how components relate to each other, and where the architecture breaks down or deviates from its intended design.

## Sub-Concerns

### 1. Coupling & Dependencies
- Circular dependencies between modules/packages
- Tight coupling between layers that should be independent
- God modules/classes that everything depends on
- Inappropriate cross-boundary imports (frontend importing backend code, etc.)
- Hidden dependencies (implicit coupling through shared state, global variables)

### 2. Layering & Separation of Concerns
- Business logic in controllers/routes/handlers
- Data access logic mixed into UI components
- Presentation logic in service layers
- Missing abstraction layers (direct DB calls from route handlers)
- Framework code leaking into domain logic

### 3. Module Boundaries
- Unclear module boundaries (what belongs where?)
- Modules that have grown too large (doing too many things)
- Modules that are too granular (unnecessary fragmentation)
- Shared code that should be extracted vs. duplicated code that should be consolidated
- Boundary violations (reaching into another module's internals)

### 4. Patterns & Consistency
- Inconsistent architectural patterns across similar modules
- Started-but-abandoned architectural migrations
- Mixed paradigms without clear reasoning (some modules use pattern A, others pattern B)
- Missing patterns where they'd add value (no repository pattern, no service layer, etc.)

### 5. Scalability & Extensibility
- Hard-coded assumptions that limit scaling
- Designs that make adding new features unnecessarily difficult
- Missing extension points where the system clearly needs them
- Monolithic components that should be decomposed

### 6. API Design (Internal)
- Inconsistent internal API contracts between modules
- Overly complex interfaces
- Leaky abstractions (implementation details exposed in interfaces)
- Missing interface definitions / contracts

## What to Look For

- Entry points (main, index, app files) — understand the top-level structure
- Import/require statements — map dependency flow
- Directory structure — does it reflect the architecture or fight against it?
- Configuration — how are modules wired together?
- Shared state — globals, singletons, event buses
- Cross-boundary communication — how do boundaries talk to each other?

## What to Skip

- Internal implementation details that are well-encapsulated
- Architectural choices that are clearly intentional and well-executed
- Simple applications that don't need complex architecture

## Context to Include

For each finding, note:
- What the current structure is
- What it implies (why this is notable)
- Which files/modules are involved
- How widespread the pattern is (isolated incident vs. systemic)