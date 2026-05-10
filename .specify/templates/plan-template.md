# Implementation Plan: [FEATURE]

**Branch**: `[###-feature-name]` | **Date**: [DATE] | **Spec**: [link]
**Input**: Feature specification from `/specs/[###-feature-name]/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

[Extract from feature spec: primary requirement + technical approach from research]

## Technical Context

<!--
  ACTION REQUIRED: Replace the content in this section with the technical details
  for the project. The structure here is presented in advisory capacity to guide
  the iteration process.
-->

**Language/Version**: TypeScript 5.9, Angular 21 or NEEDS CLARIFICATION  
**Primary Dependencies**: Angular, RxJS, Tailwind CSS, Vitest or NEEDS CLARIFICATION  
**Storage**: [if applicable, e.g., PostgreSQL, CoreData, files or N/A]  
**Testing**: Vitest via Angular CLI (`npm test`), route/user-journey checks, AXE or NEEDS CLARIFICATION  
**Target Platform**: Browser SPA or NEEDS CLARIFICATION
**Project Type**: Angular single-page application  
**Performance Goals**: Lazy-loaded route bundles and responsive user journeys or NEEDS CLARIFICATION  
**Constraints**: Clean Architecture boundaries, TDD, WCAG AA/AXE, strict TypeScript, Angular 21 native patterns  
**Scale/Scope**: [domain-specific, e.g., 10k users, 1M LOC, 50 screens or NEEDS CLARIFICATION]

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

- **Clean Architecture**: Plan identifies affected feature boundary under
  `src/app/features/[feature]/` and preserves dependency direction:
  presentation -> application -> domain, with infrastructure implementing ports.
- **Angular 21 Native Patterns**: Plan uses standalone Angular defaults, signals,
  `input()`/`output()`, `computed()`, `inject()`, native control flow, OnPush
  components, lazy routes, and no NgModules or explicit `standalone: true`.
- **TDD**: Plan defines failing tests to write before implementation for each user
  story, including domain/use-case unit tests and at least one independently
  executable acceptance or integration test per story.
- **Accessibility**: Plan lists WCAG AA and AXE validation for every changed
  user-facing journey, including keyboard, focus, names, semantics, and contrast.
- **Simplicity and Performance**: Plan justifies any new abstraction, shared state,
  eager-loaded route, or cross-feature dependency with a measurable need.

## Project Structure

### Documentation (this feature)

```text
specs/[###-feature]/
├── plan.md              # This file (/speckit-plan command output)
├── research.md          # Phase 0 output (/speckit-plan command)
├── data-model.md        # Phase 1 output (/speckit-plan command)
├── quickstart.md        # Phase 1 output (/speckit-plan command)
├── contracts/           # Phase 1 output (/speckit-plan command)
└── tasks.md             # Phase 2 output (/speckit-tasks command - NOT created by /speckit-plan)
```

### Source Code (repository root)
<!--
  ACTION REQUIRED: Replace the placeholder tree below with the concrete layout
  for this feature. Delete unused options and expand the chosen structure with
  real paths (e.g., apps/admin, packages/something). The delivered plan must
  not include Option labels.
-->

```text
src/app/
├── app.config.ts
├── app.routes.ts
├── core/
├── features/[feature]/
│   ├── application/
│   ├── domain/
│   ├── infrastructure/
│   └── presentation/
└── shared/

src/app/features/[feature]/
├── domain/[name].spec.ts
├── application/[use-case].spec.ts
└── presentation/[component].spec.ts
```

**Structure Decision**: [Document the selected structure and reference the real
directories captured above]

## Complexity Tracking

> **Fill ONLY if Constitution Check has violations that must be justified**

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| [e.g., 4th project] | [current need] | [why 3 projects insufficient] |
| [e.g., Repository pattern] | [specific problem] | [why direct DB access insufficient] |
