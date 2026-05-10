<!--
Sync Impact Report
Version change: template -> 1.0.0
Modified principles:
- Template principle 1 -> I. Clean Architecture Boundaries
- Template principle 2 -> II. Angular 21 Native Patterns
- Template principle 3 -> III. Test-First Delivery (NON-NEGOTIABLE)
- Template principle 4 -> IV. Accessibility and UX Quality Gates
- Template principle 5 -> V. Simplicity, Performance, and Maintainability
Added sections:
- Technology and Architecture Constraints
- Development Workflow and Quality Gates
Removed sections:
- Placeholder-only template guidance
Templates requiring updates:
- ✅ .specify/templates/plan-template.md
- ✅ .specify/templates/spec-template.md
- ✅ .specify/templates/tasks-template.md
- ✅ .specify/templates/checklist-template.md
- ⚠ .specify/templates/commands/*.md not present in this repository
- ✅ README.md
- ✅ AGENTS.md reviewed; no change required
Follow-up TODOs: None
-->
# Speckit Angular Demo Constitution

## Core Principles

### I. Clean Architecture Boundaries
Every feature MUST preserve a clear dependency direction: presentation depends on
application use cases, application depends on domain contracts, and infrastructure
implements those contracts. Domain models, business rules, and use cases MUST NOT
import Angular APIs, browser APIs, HTTP clients, routing, storage implementations, or
component state. Infrastructure code MUST remain replaceable behind ports so tests can
exercise behavior without real network, persistence, or framework side effects.

Rationale: Clean boundaries keep the SPA scalable as features grow, make business
behavior testable in isolation, and prevent UI framework choices from leaking into the
core model.

### II. Angular 21 Native Patterns
Angular code MUST use standalone Angular 21 patterns and strict TypeScript. Components
MUST use `ChangeDetectionStrategy.OnPush`, signal-based local state, `input()` and
`output()` for component contracts, `computed()` for derived state, `inject()` for
dependency access, and native template control flow (`@if`, `@for`, `@switch`). Code
MUST NOT set `standalone: true`, use NgModules for feature composition, use
`@HostBinding` or `@HostListener`, use `ngClass` or `ngStyle`, or introduce `any`
without a documented migration task. Static images MUST use `NgOptimizedImage` unless
they are inline base64 images.

Rationale: These rules align the project with Angular 21 defaults, reduce change
detection cost, and keep templates predictable and accessible.

### III. Test-First Delivery (NON-NEGOTIABLE)
All production behavior MUST begin with failing tests before implementation. Each user
story MUST include at least one independently executable acceptance or integration test
and focused unit tests for domain rules, use cases, and non-trivial presentation logic.
The required cycle is red, green, refactor: write the test, verify it fails for the
expected reason, implement the smallest passing change, then refactor while tests remain
green. Bug fixes MUST include a regression test that fails before the fix.

Rationale: TDD is the primary control for Clean Architecture compliance and protects
the SPA from regressions while it evolves.

### IV. Accessibility and UX Quality Gates
Every user-facing change MUST meet WCAG AA and pass automated AXE checks before it is
accepted. Interactive controls MUST have accessible names, visible focus states,
keyboard paths, semantic markup, and correct ARIA only where native HTML is
insufficient. Visual design MUST maintain readable contrast, responsive layouts, and no
text or control overlap at supported viewport sizes.

Rationale: Accessibility is a product requirement, not a polish task. Building it into
each feature avoids costly retrofits and produces a more robust UI for all users.

### V. Simplicity, Performance, and Maintainability
Features MUST choose the simplest design that satisfies the current specification and
preserves the architecture boundaries above. Shared abstractions MUST be introduced
only after repeated behavior or a real cross-feature contract exists. Feature bundles
MUST be lazy loaded where routing allows it, state transformations MUST be pure, and
expensive derived values MUST use signals or memoized selectors. Performance work MUST
state the measurable target it protects.

Rationale: A small Angular SPA can become difficult to change if abstractions arrive
too early or performance is treated as an afterthought.

## Technology and Architecture Constraints

This project is a single-page application built with Angular 21, TypeScript 5.9,
RxJS 7.8, Vitest, Tailwind CSS 4, and the Angular CLI. New feature code MUST follow this
default source layout unless a plan documents a narrower existing location:

```text
src/app/
├── core/                 # App-level providers, platform services, shared adapters
├── features/[feature]/   # Route-level feature boundary
│   ├── application/      # Use cases, DTO mapping, facades, ports
│   ├── domain/           # Entities, value objects, domain services, contracts
│   ├── infrastructure/   # HTTP/storage adapters implementing application ports
│   └── presentation/     # Components, routes, view models, UI-only state
└── shared/               # Reusable UI and utilities with no feature business rules
```

Feature routes MUST be lazy loaded from `src/app/app.routes.ts` or a feature route file.
Dependencies MUST point inward: presentation can call application, application can call
domain, and infrastructure can depend on application/domain contracts. Domain and
application code MUST remain usable in Vitest without Angular TestBed unless the code
explicitly integrates with Angular.

## Development Workflow and Quality Gates

Each specification MUST define independently testable user stories, measurable success
criteria, accessibility expectations, and the Clean Architecture boundary affected by
the work. Each implementation plan MUST pass the Constitution Check before research and
again after design. Each generated task list MUST order work test-first per story and
MUST include explicit tasks for architecture boundaries, accessibility checks, and
quality commands.

The required verification for a completed feature is:

- `npm test` or the Angular CLI test target for all relevant unit and integration tests.
- A build verification with `npm run build` before merge or delivery.
- AXE or equivalent accessibility validation for changed user journeys.
- Manual or automated route-level verification for each accepted user story.

Any skipped gate MUST be recorded in the feature plan with a concrete reason, owner,
and follow-up task before the work can be considered complete.

## Governance

This constitution supersedes conflicting project guidance for architecture, Angular
usage, testing, accessibility, and quality gates. Amendments require a documented change
to this file, a Sync Impact Report, and updates to affected Speckit templates or runtime
guidance in the same change set.

Versioning follows semantic versioning:

- MAJOR for removing or redefining a principle in a backward-incompatible way.
- MINOR for adding a principle, governance section, mandatory gate, or materially
  expanding constraints.
- PATCH for clarifications, wording fixes, or non-semantic refinements.

Compliance is reviewed during `/speckit-plan`, `/speckit-tasks`, implementation, and
code review. Plans and tasks that violate a MUST rule require an explicit Complexity
Tracking entry explaining the violation, the simpler alternative considered, and the
time-bound mitigation.

**Version**: 1.0.0 | **Ratified**: 2026-05-10 | **Last Amended**: 2026-05-10
