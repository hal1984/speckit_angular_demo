---

description: "Task list template for feature implementation"
---

# Tasks: [FEATURE NAME]

**Input**: Design documents from `/specs/[###-feature-name]/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/

**Tests**: Tests are mandatory. This project follows TDD; every user story MUST
start with failing tests before implementation tasks.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Path Conventions

- **Angular SPA feature**: `src/app/features/[feature]/`
- **Domain**: `src/app/features/[feature]/domain/`
- **Application**: `src/app/features/[feature]/application/`
- **Infrastructure**: `src/app/features/[feature]/infrastructure/`
- **Presentation**: `src/app/features/[feature]/presentation/`
- **Shared app code**: `src/app/core/` or `src/app/shared/` only when justified by plan.md

<!-- 
  ============================================================================
  IMPORTANT: The tasks below are SAMPLE TASKS for illustration purposes only.
  
  The /speckit-tasks command MUST replace these with actual tasks based on:
  - User stories from spec.md (with their priorities P1, P2, P3...)
  - Feature requirements from plan.md
  - Entities from data-model.md
  - Endpoints from contracts/
  
  Tasks MUST be organized by user story so each story can be:
  - Implemented independently
  - Tested independently
  - Delivered as an MVP increment
  
  DO NOT keep these sample tasks in the generated tasks.md file.
  ============================================================================
-->

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization and basic structure

- [ ] T001 Create Angular feature structure per implementation plan
- [ ] T002 Configure lazy route entry for [feature] in src/app/app.routes.ts or feature routes
- [ ] T003 [P] Confirm Vitest, build, and accessibility tooling commands for the feature

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Core infrastructure that MUST be complete before ANY user story can be implemented

**⚠️ CRITICAL**: No user story work can begin until this phase is complete

Examples of foundational tasks (adjust based on your project):

- [ ] T004 Define domain entities/value objects and ports shared by stories in src/app/features/[feature]/domain/
- [ ] T005 [P] Define application use-case contracts and DTO mapping in src/app/features/[feature]/application/
- [ ] T006 [P] Define infrastructure adapter boundaries in src/app/features/[feature]/infrastructure/
- [ ] T007 Create presentation route shell with OnPush, signals, and accessible landmarks in src/app/features/[feature]/presentation/
- [ ] T008 Configure shared error, loading, and empty-state handling for the feature
- [ ] T009 Verify dependency direction: presentation -> application -> domain, infrastructure implements ports

**Checkpoint**: Foundation ready - user story implementation can now begin in parallel

---

## Phase 3: User Story 1 - [Title] (Priority: P1) 🎯 MVP

**Goal**: [Brief description of what this story delivers]

**Independent Test**: [How to verify this story works on its own]

### Tests for User Story 1 ⚠️

> **NOTE: Write these tests FIRST, ensure they FAIL before implementation**

- [ ] T010 [P] [US1] Failing domain/use-case test in src/app/features/[feature]/domain/[name].spec.ts or application/[use-case].spec.ts
- [ ] T011 [P] [US1] Failing presentation or route integration test in src/app/features/[feature]/presentation/[component].spec.ts
- [ ] T012 [US1] Verify the new US1 tests fail for the expected reason

### Implementation for User Story 1

- [ ] T013 [P] [US1] Implement domain model/rules in src/app/features/[feature]/domain/
- [ ] T014 [US1] Implement application use case in src/app/features/[feature]/application/
- [ ] T015 [US1] Implement infrastructure adapter if required in src/app/features/[feature]/infrastructure/
- [ ] T016 [US1] Implement OnPush signal-based presentation in src/app/features/[feature]/presentation/
- [ ] T017 [US1] Add validation, loading, empty, and error states
- [ ] T018 [US1] Run US1 tests and refactor with tests green
- [ ] T019 [US1] Run AXE/accessibility validation for the US1 journey

**Checkpoint**: At this point, User Story 1 should be fully functional and testable independently

---

## Phase 4: User Story 2 - [Title] (Priority: P2)

**Goal**: [Brief description of what this story delivers]

**Independent Test**: [How to verify this story works on its own]

### Tests for User Story 2 ⚠️

- [ ] T020 [P] [US2] Failing domain/use-case test in src/app/features/[feature]/domain/ or application/
- [ ] T021 [P] [US2] Failing presentation or route integration test in src/app/features/[feature]/presentation/
- [ ] T022 [US2] Verify the new US2 tests fail for the expected reason

### Implementation for User Story 2

- [ ] T023 [P] [US2] Implement domain/application behavior in the appropriate Clean Architecture layer
- [ ] T024 [US2] Implement infrastructure adapter changes if required
- [ ] T025 [US2] Implement OnPush signal-based presentation changes
- [ ] T026 [US2] Integrate with User Story 1 components only through application contracts if needed
- [ ] T027 [US2] Run tests and AXE/accessibility validation for the US2 journey

**Checkpoint**: At this point, User Stories 1 AND 2 should both work independently

---

## Phase 5: User Story 3 - [Title] (Priority: P3)

**Goal**: [Brief description of what this story delivers]

**Independent Test**: [How to verify this story works on its own]

### Tests for User Story 3 ⚠️

- [ ] T028 [P] [US3] Failing domain/use-case test in src/app/features/[feature]/domain/ or application/
- [ ] T029 [P] [US3] Failing presentation or route integration test in src/app/features/[feature]/presentation/
- [ ] T030 [US3] Verify the new US3 tests fail for the expected reason

### Implementation for User Story 3

- [ ] T031 [P] [US3] Implement domain/application behavior in the appropriate Clean Architecture layer
- [ ] T032 [US3] Implement infrastructure adapter changes if required
- [ ] T033 [US3] Implement OnPush signal-based presentation changes
- [ ] T034 [US3] Run tests and AXE/accessibility validation for the US3 journey

**Checkpoint**: All user stories should now be independently functional

---

[Add more user story phases as needed, following the same pattern]

---

## Phase N: Polish & Cross-Cutting Concerns

**Purpose**: Improvements that affect multiple user stories

- [ ] TXXX [P] Documentation updates in README.md or specs/[###-feature]/quickstart.md
- [ ] TXXX Code cleanup and refactoring with tests green
- [ ] TXXX Performance optimization across all stories with measurable target
- [ ] TXXX [P] Additional unit and integration tests for uncovered branches
- [ ] TXXX Security and privacy hardening
- [ ] TXXX Run `npm test`
- [ ] TXXX Run `npm run build`
- [ ] TXXX Run quickstart.md validation

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion - BLOCKS all user stories
- **User Stories (Phase 3+)**: All depend on Foundational phase completion
  - User stories can then proceed in parallel (if staffed)
  - Or sequentially in priority order (P1 → P2 → P3)
- **Polish (Final Phase)**: Depends on all desired user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational (Phase 2) - No dependencies on other stories
- **User Story 2 (P2)**: Can start after Foundational (Phase 2) - May integrate with US1 but should be independently testable
- **User Story 3 (P3)**: Can start after Foundational (Phase 2) - May integrate with US1/US2 but should be independently testable

### Within Each User Story

- Tests MUST be written and FAIL before implementation
- Domain before application
- Application before infrastructure adapters and presentation integration
- Core implementation before integration
- Story complete before moving to next priority

### Parallel Opportunities

- All Setup tasks marked [P] can run in parallel
- All Foundational tasks marked [P] can run in parallel (within Phase 2)
- Once Foundational phase completes, all user stories can start in parallel (if team capacity allows)
- All tests for a user story marked [P] can run in parallel
- Domain files, use-case tests, and presentation tests within a story marked [P]
  can run in parallel when they touch different files
- Different user stories can be worked on in parallel by different team members

---

## Parallel Example: User Story 1

```bash
# Launch all tests for User Story 1 together:
Task: "Failing domain/use-case test in src/app/features/[feature]/domain/[name].spec.ts"
Task: "Failing presentation test in src/app/features/[feature]/presentation/[component].spec.ts"

# Launch independent Clean Architecture slices for User Story 1:
Task: "Implement domain model/rules in src/app/features/[feature]/domain/"
Task: "Implement application use case in src/app/features/[feature]/application/"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational (CRITICAL - blocks all stories)
3. Complete Phase 3: User Story 1
4. **STOP and VALIDATE**: Test User Story 1 independently
5. Deploy/demo if ready

### Incremental Delivery

1. Complete Setup + Foundational → Foundation ready
2. Add User Story 1 → Test independently → Deploy/Demo (MVP!)
3. Add User Story 2 → Test independently → Deploy/Demo
4. Add User Story 3 → Test independently → Deploy/Demo
5. Each story adds value without breaking previous stories

### Parallel Team Strategy

With multiple developers:

1. Team completes Setup + Foundational together
2. Once Foundational is done:
   - Developer A: User Story 1
   - Developer B: User Story 2
   - Developer C: User Story 3
3. Stories complete and integrate independently

---

## Notes

- [P] tasks = different files, no dependencies
- [Story] label maps task to specific user story for traceability
- Each user story should be independently completable and testable
- Verify tests fail before implementing
- Commit after each task or logical group
- Stop at any checkpoint to validate story independently
- Avoid: vague tasks, same file conflicts, cross-story dependencies that break independence
