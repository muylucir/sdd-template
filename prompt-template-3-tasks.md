# Prompt Template: Generate Implementation Tasks from Requirements and Design

## Role
You are a technical project manager and lead developer responsible for breaking down architectural designs into concrete, actionable implementation tasks with clear dependencies and validation points.

## Task
Convert the provided requirements and design documents into a detailed Implementation Plan (tasks.md) that organizes all implementation work into a logical sequence of tasks with checkboxes, subtasks, requirements traceability, and comprehensive testing (unit, integration, and E2E tests).

## Input Format
You will receive:
1. **requirements.md**: Complete requirements document with all acceptance criteria (located at `.kiro/specs/requirements.md`)
2. **design.md**: Complete design document with architecture, interfaces, and testing strategy (located at `.kiro/specs/design.md`)

## Output Format

Generate a `tasks.md` file with the following structure:

```markdown
# Implementation Plan

- [ ] [N]. [Major Task Name]
  - [Brief description of what this task accomplishes]
  - [Technology/component details]
  - _Requirements: [comma-separated list of requirement numbers]_

- [ ] [N]. [Major Task Name with Subtasks]
- [ ] [N.1] [Subtask Name]
  - [Description]
  - _Requirements: [requirement numbers]_

- [ ] [N.2] [Subtask Name - Unit Tests]
  - [Test scenarios covering core logic, edge cases, error handling]
  - _Requirements: [requirement numbers]_

- [ ] [N]. Checkpoint - [Checkpoint Description]
  - [What to verify at this checkpoint]

[Continue with all implementation tasks...]
```

## Guidelines

### 1. Task Organization Phases

Break down implementation into these standard phases:

#### Phase 1: Foundation Setup
- Project structure and dependencies
- Type definitions and interfaces
- Database schema and ORM setup
- Configuration files

#### Phase 2: Core Services Implementation
- For each module in the design document, create tasks for:
  - Service implementation
  - Unit tests for that module (core logic, edge cases, error handling)
  - Integration tests for that module (database operations, API endpoints)
- Order by dependency (e.g., auth before features that need auth)

#### Phase 3: API Layer
- API routes/endpoints for each module
- API integration tests
- Error handling and validation

#### Phase 4: User Interface (if applicable)
- UI components for each feature
- Form validation
- User feedback mechanisms

#### Phase 5: End-to-End Testing & Deployment
- E2E tests for critical user workflows
- Cross-module integration validation
- Deployment configuration
- Final smoke tests

#### Checkpoints
- Add checkpoint tasks after completing major phases
- Checkpoints ensure all tests pass before proceeding

### 2. Task Numbering System

Use hierarchical numbering:
- Major tasks: `1.`, `2.`, `3.`, etc.
- Subtasks: `1.1`, `1.2`, `1.3`, etc.
- Further breakdown: `1.1.1`, `1.1.2`, etc. (if needed)

### 3. Task Checkbox Format

```markdown
- [ ] N. Task name
- [x] N. Completed task name
- [-] N. In-progress task name
```

Start with all tasks unchecked `- [ ]`.

### 4. Task Description Format

Each major task should include:
```markdown
- [ ] N. [Clear, action-oriented task name]
  - [1-3 sentence description of what this task accomplishes]
  - [Key technical details: which files, components, or systems are involved]
  - [Any important notes about implementation approach]
  - _Requirements: [comma-separated requirement numbers this task addresses]_
```

Each subtask should include:
```markdown
- [ ] N.M [Subtask name]
  - [1-2 sentence description]
  - _Requirements: [requirement numbers]_
```

### 5. Unit Test Tasks

For each module implementation, create unit test tasks:

```markdown
- [ ] N.M Write unit tests for [module name]
  - Test [scenario 1: valid input handling]
  - Test [scenario 2: invalid input and error cases]
  - Test [scenario 3: edge cases and boundary conditions]
  - Test [scenario 4: business logic correctness]
  - _Requirements: [requirement numbers]_
```

List specific test scenarios based on:
- Core business logic and calculations
- Edge cases mentioned in requirements
- Error conditions and exception handling
- Boundary conditions
- Input validation

**Key Principles**:
- Tests should be fast (no database, no network)
- Mock external dependencies
- One test per scenario
- Clear test names

### 6. Integration Test Tasks

For each module with external dependencies (database, APIs, etc.), create integration test tasks:

```markdown
- [ ] N.M Write integration tests for [module name] API
  - Test [API endpoint 1] with actual database
  - Test [API endpoint 2] authentication flow
  - Test [scenario 3: concurrent requests handling]
  - Test [scenario 4: transaction rollback on error]
  - _Requirements: [requirement numbers]_
```

List specific integration scenarios based on:
- API endpoints and their complete request/response cycles
- Database operations (create, read, update, delete)
- Authentication and authorization flows
- External service integrations
- Error handling across system boundaries

**Key Principles**:
- Use real database (test database or in-memory)
- Test actual HTTP requests/responses
- Verify data persistence
- Clean up test data after each test

### 7. E2E Test Tasks

For critical user workflows, create E2E test tasks (usually in Phase 5):

```markdown
- [ ] N. Write E2E tests for critical user workflows
  - Test [complete user workflow 1: e.g., user registration and login]
  - Test [complete user workflow 2: e.g., create, edit, delete resource]
  - Test [complete user workflow 3: e.g., multi-step business process]
  - _Requirements: [requirement numbers]_
```

List specific E2E scenarios based on:
- Critical business processes from start to finish
- Most common user journeys
- Multi-step workflows spanning multiple pages/modules
- Error recovery scenarios from user perspective

**Key Principles**:
- Test from user's perspective (UI interactions)
- Cover critical paths, not every detail
- Fewer but more valuable tests
- Run in test/staging environment

### 8. Requirements Traceability

Every task must reference the requirements it implements:

```markdown
_Requirements: 1.1, 1.2, 1.3_
```

or

```markdown
_Requirements: All_
```

This ensures:
- Complete coverage of all requirements
- Easy tracking of which tasks implement which features
- Validation that nothing is missed

### 9. Checkpoint Tasks

Add checkpoint tasks at strategic points:

```markdown
- [ ] N. Checkpoint - [What is being validated]
  - [Specific things to verify]
  - [What to do if validation fails]
```

Common checkpoint locations:
- After foundation setup (verify project runs)
- After each major module (verify all unit and integration tests pass)
- Before UI implementation (verify all APIs work)
- Before deployment (verify full test suite passes including E2E)

Standard checkpoint format:
```markdown
- [ ] N. Checkpoint - Ensure all tests pass
  - Run unit tests and verify they all pass
  - Run integration tests and verify API functionality
  - Fix any failing tests before proceeding
  - Ask the user if questions arise
```

**Key Validation Points**:
- Unit tests pass (fast feedback on logic)
- Integration tests pass (API and database work correctly)
- No compilation or linting errors
- Application runs without crashes

### 10. Task Sequencing Rules

#### Dependencies First
- Set up project before implementing features
- Implement authentication before protected features
- Implement data models before services that use them
- Implement services before APIs that use them
- Implement APIs before UIs that call them

#### Logical Grouping
- Group related tasks together (e.g., all tasks for a module)
- Keep implementation and testing tasks adjacent
- Keep property tests and unit tests together under their module

#### Incremental Validation
- Interleave implementation with testing
- Don't defer all testing to the end
- Add checkpoints to validate progress

### 11. Task Granularity

#### Major Tasks (Top Level)
Should represent significant milestones:
- "Set up project structure and dependencies"
- "Implement Authentication Service"
- "Implement Reservation Management Module"
- "Create API routes for room management"

#### Subtasks (Second Level)
Should represent concrete, completable work items:
- "Create authentication service with NextAuth.js"
- "Write property test for authentication"
- "Implement `createReservation` with validation"
- "Create POST /api/rooms endpoint"

#### Further Breakdown (Third Level, if needed)
Only when a subtask is complex:
- "Configure credential provider"
- "Add password hashing"
- "Implement session management"

### 12. Common Task Patterns

#### For Service Implementation:
```markdown
- [ ] N. Implement [Module Name] Service
- [ ] N.1 Create [module] service with [operations]
  - Implement [function 1] with [details]
  - Implement [function 2] with [details]
  - Add [supporting functionality]
  - _Requirements: [numbers]_

- [ ] N.2 Write unit tests for [module] service
  - Test [scenario 1: valid input handling]
  - Test [scenario 2: error handling and validation]
  - Test [scenario 3: edge cases]
  - _Requirements: [numbers]_

- [ ] N.3 Write integration tests for [module] API
  - Test [API endpoint 1] with database
  - Test [API endpoint 2] authentication
  - _Requirements: [numbers]_
```

#### For API Implementation:
```markdown
- [ ] N. Create API routes for [feature]
- [ ] N.1 Implement [feature] API endpoints
  - Create [METHOD] /api/[path] for [purpose]
  - Create [METHOD] /api/[path] for [purpose]
  - Add [authorization/validation] middleware
  - _Requirements: [numbers]_

- [ ] N.2 Write API integration tests for [feature]
  - Test [scenario 1]
  - Test [scenario 2]
```

#### For UI Implementation:
```markdown
- [ ] N. Implement [Feature] UI components
- [ ] N.1 Create [feature] layout and components
  - Create [Component1] component
  - Implement [Component2] for [purpose]
  - Add [functionality]
  - _Requirements: [numbers]_

- [ ] N.2 Write component tests for [feature] UI
  - Test [component rendering and interactions]
  - Test [form validation and submission]
  - _Requirements: [numbers]_
```

#### For E2E Testing (Phase 5):
```markdown
- [ ] N. Write E2E tests for critical workflows
- [ ] N.1 E2E test for [user workflow 1]
  - Test complete flow: [step 1] → [step 2] → [step 3]
  - Verify [expected outcome]
  - _Requirements: [numbers]_

- [ ] N.2 E2E test for [user workflow 2]
  - Test [multi-step business process]
  - Verify [data persistence across steps]
  - _Requirements: [numbers]_
```

### 13. Extracting Tasks from Design Document

#### From Components and Interfaces Section:
For each module → Create implementation task + unit test tasks + integration test tasks

#### From Correctness Properties Section:
For each property → Ensure it's covered by unit and/or integration tests

#### From Testing Strategy Section:
- Unit tests → Create unit test tasks for each module
- Integration tests → Create integration test tasks for APIs and database operations
- E2E tests → Create E2E test tasks for critical user workflows
- Test data management → Include in test setup tasks

#### From Error Handling Section:
- Error handling strategy → Create tasks for error utilities
- Client validation → Create tasks under UI implementation
- Server validation → Include in service implementation tasks

#### From Architecture Diagram:
- Each layer/component → Verify there are implementation tasks
- Dependencies between components → Ensure task ordering respects dependencies

### 14. Complete Coverage Checklist

Before finalizing, verify:
- [ ] Every module from design.md has an implementation task
- [ ] Every module has unit test tasks
- [ ] Every module with external dependencies has integration test tasks
- [ ] Critical user workflows have E2E test tasks
- [ ] Every API endpoint from design has an implementation task
- [ ] Every UI component from design has an implementation task
- [ ] Requirements traceability is complete (all requirements referenced)
- [ ] Tasks are ordered by dependencies
- [ ] Checkpoints are placed at logical milestones
- [ ] Project setup tasks are at the beginning
- [ ] E2E tests and deployment tasks are at the end
- [ ] Testing tasks are distributed throughout (not all deferred to the end)

### 15. Special Considerations

#### Testing Strategy Integration
- Unit tests should be written **immediately after** each service implementation
- Integration tests should be written after API endpoints are implemented
- E2E tests should be written in Phase 5 after all features are complete
- Explicitly state which requirements each test validates

#### Technology-Specific Tasks
- Adjust task descriptions to match the technology stack
- Include framework-specific setup steps
- Reference specific libraries or tools

#### Incremental Development
- Tasks should support incremental development
- Each task should leave the system in a working (or testable) state
- Avoid long task sequences without validation

### 16. Example Task Extraction

**From design.md:**
```markdown
### 3. Reservation Management Module

**책임**: 예약 생성, 수정, 취소 및 조회

**인터페이스**:
interface ReservationService {
  createReservation(reservation: CreateReservationDto): Promise<Reservation>;
  updateReservation(reservationId: string, updates: UpdateReservationDto): Promise<Reservation>;
  cancelReservation(reservationId: string, userId: string): Promise<void>;
}

### Correctness Properties

### Property 4: Reservation persistence completeness
*For any* valid reservation created, querying the database should return a reservation record containing the user ID, room ID, start time, end time, and title.
**Validates: Requirements 2.5**

### Testing Strategy

#### Unit Testing
- Test createReservation with valid/invalid data
- Test conflict detection and overlap scenarios
- Test cancellation and update flows

#### Integration Testing
- Test POST /api/reservations endpoint with database
- Test concurrent reservation requests
```

**To tasks.md:**
```markdown
- [ ] 7. Implement Reservation Service
- [ ] 7.1 Create reservation service with core operations
  - Implement `createReservation` with validation and conflict checking
  - Implement `updateReservation` with availability validation
  - Implement `cancelReservation` with status update
  - Implement query functions: `getReservation`, `getUserReservations`, `getRoomReservations`
  - Implement `checkAvailability` with overlap detection
  - Add database transaction support for concurrent requests
  - _Requirements: 2.1, 2.2, 2.3, 2.4, 2.5, 3.1, 3.2, 3.3, 3.4, 3.5, 4.1, 4.2, 4.3, 4.4_

- [ ] 7.2 Write unit tests for reservation service
  - Test reservation creation with valid data
  - Test validation errors for invalid input (missing fields, invalid dates)
  - Test conflict detection scenarios (overlapping reservations)
  - Test cancellation flow (status update, user authorization)
  - Test update validation (availability check, permission check)
  - Test edge cases (same start/end time, past dates, etc.)
  - _Requirements: 2.1, 2.2, 2.3, 2.4, 2.5_

- [ ] 7.3 Write integration tests for reservation API
  - Test POST /api/reservations endpoint with actual database
  - Test GET /api/reservations/:id retrieval with database query
  - Test concurrent reservation requests for same time slot
  - Test reservation persistence completeness (Property 4: all fields saved correctly)
  - Test transaction rollback on conflict errors
  - _Requirements: 2.5, 3.1, 3.2_
```

## Important Notes
- Tasks should be actionable and specific
- Every requirement must be covered by at least one task
- Unit tests should be written immediately after the code they test (not deferred)
- Integration tests should be written after API endpoints are implemented
- E2E tests should be written in the final phase for critical user workflows
- Checkpoints ensure quality gates are met
- Task order should respect dependencies
- Group related tasks together for clarity
- Testing strategy should be practical: fast unit tests, thorough integration tests, selective E2E tests

## Now Generate

Please provide:
1. The complete `requirements.md` content
2. The complete `design.md` content

And I will generate a comprehensive `tasks.md` implementation plan following this template.

**Important Requirements:**
- The generated document must be written in **Korean (한글)**
- Task descriptions, technical terms, and code references should be in Korean
- **CRITICAL**: Follow practical testing approach:
  - Unit tests immediately after each module implementation
  - Integration tests after API endpoints are completed
  - E2E tests in Phase 5 for critical user workflows only
  - Focus on test quality over quantity
- Save the generated file as `.kiro/specs/tasks.md`
