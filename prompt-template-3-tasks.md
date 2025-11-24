# Prompt Template: Generate Implementation Tasks from Requirements and Design

## Role
You are a technical project manager and lead developer responsible for breaking down architectural designs into concrete, actionable implementation tasks with clear dependencies and validation points.

## Task
Convert the provided requirements and design documents into a detailed Implementation Plan (tasks.md) that organizes all implementation work into a logical sequence of tasks with checkboxes, subtasks, requirements traceability, and property-based testing integration.

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

- [ ] [N.2] [Subtask Name - Property Test]
  - **Property [X]: [Property name]**
  - **Validates: Requirements [requirement numbers]**

- [ ] [N.3] [Subtask Name - Unit Tests]
  - [Test scenarios]

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
  - Property-based tests for that module
  - Unit tests for that module
- Order by dependency (e.g., auth before features that need auth)

#### Phase 3: API Layer
- API routes/endpoints for each module
- API integration tests
- Error handling and validation

#### Phase 4: User Interface (if applicable)
- UI components for each feature
- Form validation
- User feedback mechanisms

#### Phase 5: Integration & Deployment
- End-to-end integration tests
- Deployment configuration
- Final validation

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

### 5. Property-Based Test Tasks

For **every** correctness property in the design document, create a subtask:

```markdown
- [ ] N.M Write property test for [property name]
  - **Property [X]: [Property name from design.md]**
  - **Validates: Requirements [requirement numbers]**
```

These tasks should be:
- Grouped under the related service/module implementation task
- Clearly labeled with the property number and name
- Explicit about which requirements they validate
- Reference the iteration count from design.md (DO NOT hardcode specific numbers like 100 or 1000)

### 6. Unit Test Tasks

After property tests for a module, add unit test tasks:

```markdown
- [ ] N.M Write unit tests for [module name]
  - [Test scenario 1]
  - [Test scenario 2]
  - [Test scenario 3]
```

List specific test scenarios based on:
- Edge cases mentioned in requirements
- Error conditions
- Boundary conditions
- Common use cases

### 7. Requirements Traceability

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

### 8. Checkpoint Tasks

Add checkpoint tasks at strategic points:

```markdown
- [ ] N. Checkpoint - [What is being validated]
  - [Specific things to verify]
  - [What to do if validation fails]
```

Common checkpoint locations:
- After foundation setup (verify project runs)
- After each major module (verify tests pass)
- Before UI implementation (verify all APIs work)
- Before deployment (verify all integration tests pass)

Standard checkpoint format:
```markdown
- [ ] N. Checkpoint - Ensure all tests pass
  - Ensure all tests pass, ask the user if questions arise.
  - Property-based tests should run with the minimum iteration count specified in design.md
```

**Important**: When creating checkpoint tasks that mention property-based tests:
- DO NOT hardcode iteration counts (e.g., "1000회", "100회")
- ALWAYS reference design.md: "Property-based tests should run with the iteration count specified in design.md"
- Or use generic language: "Ensure property tests pass with configured iteration count"

### 9. Task Sequencing Rules

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

### 10. Task Granularity

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

### 11. Common Task Patterns

#### For Service Implementation:
```markdown
- [ ] N. Implement [Module Name] Service
- [ ] N.1 Create [module] service with [operations]
  - Implement [function 1] with [details]
  - Implement [function 2] with [details]
  - Add [supporting functionality]
  - _Requirements: [numbers]_

- [ ] N.2 Write property test for [property name]
  - **Property [X]: [property name]**
  - **Validates: Requirements [numbers]**

- [ ] N.3 Write unit tests for [module] service
  - Test [scenario 1]
  - Test [scenario 2]
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

- [ ] N.2 Write integration tests for [feature] UI
  - Test [user workflow 1]
  - Test [user workflow 2]
```

### 12. Extracting Tasks from Design Document

#### From Components and Interfaces Section:
For each module → Create implementation task + property test tasks + unit test tasks

#### From Correctness Properties Section:
For each property → Create a property test task under the relevant module

#### From Testing Strategy Section:
- Unit tests → Create unit test tasks
- Property tests → Already created from properties
- Integration tests → Create integration test tasks
- Test data generators → Include in test setup tasks

#### From Error Handling Section:
- Error handling strategy → Create tasks for error utilities
- Client validation → Create tasks under UI implementation
- Server validation → Include in service implementation tasks

#### From Architecture Diagram:
- Each layer/component → Verify there are implementation tasks
- Dependencies between components → Ensure task ordering respects dependencies

### 13. Complete Coverage Checklist

Before finalizing, verify:
- [ ] Every module from design.md has an implementation task
- [ ] Every correctness property has a property test task
- [ ] Every module has unit test tasks
- [ ] Every API endpoint from design has an implementation task
- [ ] Every UI component from design has an implementation task
- [ ] Requirements traceability is complete (all requirements referenced)
- [ ] Tasks are ordered by dependencies
- [ ] Checkpoints are placed at logical milestones
- [ ] Project setup tasks are at the beginning
- [ ] Deployment tasks are at the end
- [ ] Testing tasks are distributed throughout (not all at the end)

### 14. Special Considerations

#### Property-Based Testing Integration
- Property tests should be written **immediately after** the service implementation
- Reference the exact property number and name from design.md
- Explicitly state which requirements are validated
- Use the iteration count specified in design.md (never hardcode numbers like 100 or 1000 in task descriptions)

#### Technology-Specific Tasks
- Adjust task descriptions to match the technology stack
- Include framework-specific setup steps
- Reference specific libraries or tools

#### Incremental Development
- Tasks should support incremental development
- Each task should leave the system in a working (or testable) state
- Avoid long task sequences without validation

### 15. Example Task Extraction

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

### Property 4: Reservation persistence completeness
*For any* valid reservation created, querying the database should return a reservation record containing the user ID, room ID, start time, end time, and title.
**Validates: Requirements 2.5**
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

- [ ] 7.2 Write property test for reservation persistence
  - **Property 4: Reservation persistence completeness**
  - **Validates: Requirements 2.5**

- [ ] 7.3 Write unit tests for reservation service
  - Test reservation creation with valid data
  - Test conflict detection scenarios
  - Test cancellation flow
  - Test update validation
```

## Important Notes
- Tasks should be actionable and specific
- Every requirement must be covered by at least one task
- Every property must have a corresponding test task
- Property tests should be written alongside the code they test (not deferred)
- **DO NOT hardcode property test iteration counts** - always reference design.md's specified count
- Checkpoints ensure quality gates are met
- Task order should respect dependencies
- Group related tasks together for clarity

## Now Generate

Please provide:
1. The complete `requirements.md` content
2. The complete `design.md` content

And I will generate a comprehensive `tasks.md` implementation plan following this template.

**Important Requirements:**
- The generated document must be written in **Korean (한글)**
- Task descriptions, technical terms, and code references should be in Korean
- **CRITICAL**: Do NOT hardcode property test iteration counts in task descriptions or checkpoints
  - Use: "design.md에 명시된 반복 횟수로 property test 실행"
  - NOT: "1000회 property test 실행" or "100회 반복"
- Save the generated file as `.kiro/specs/tasks.md`
