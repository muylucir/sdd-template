# Prompt Template: Generate Design Document from Requirements

## Role
You are a senior software architect specializing in translating functional requirements into comprehensive technical designs with clear architectural decisions, interfaces, and testing strategies.

## Task
Convert the provided requirements document into a detailed Design Document that specifies the system architecture, component interfaces, data models, correctness properties, and comprehensive testing strategy including property-based testing.

## Input Format
You will receive:
1. **requirements.md**: Complete requirements document with EARS notation (located at `.kiro/specs/requirements.md`)
2. **Technology Stack Information**: From the original idea.md located at `.kiro/idea/idea.md` (language/framework, database, deployment platform, etc.)

## Output Format

Generate a `design.md` file with the following structure:

```markdown
# Design Document

## Overview
[2-4 paragraph overview describing the system architecture, technology choices, and core design principles]

핵심 설계 원칙:
- **[Principle 1]**: [Description]
- **[Principle 2]**: [Description]
- **[Principle 3]**: [Description]
...

## Architecture

[Brief description of the architectural pattern being used]

```mermaid
graph TB
    subgraph "[Layer Name]"
        Component1[Component Name]
        Component2[Component Name]
    end

    subgraph "[Layer Name]"
        Component3[Component Name]
    end

    Component1 --> Component3
    Component2 --> Component3
```

### Technology Stack

- **[Category 1]**: [Technologies]
- **[Category 2]**: [Technologies]
- **[Category 3]**: [Technologies]
...

## Components and Interfaces

### [N]. [Module Name]

**책임**: [Brief description of module responsibilities]

**인터페이스**:
```[language]
[Interface/Service definitions in the specified technology stack]
```

[Repeat for each major module]

## Data Models

### [Entity Name]
```[language]
[Data model definition in the specified technology stack]
```

[Repeat for each entity]

### Database Schema

```[database-language]
[Database schema in the appropriate syntax]
```

## Correctness Properties

*A property is a characteristic or behavior that should hold true across all valid executions of a system-essentially, a formal statement about what the system should do. Properties serve as the bridge between human-readable specifications and machine-verifiable correctness guarantees.*

### Property [N]: [Property Name]
*For any* [scope], [the property statement that should always be true].
**Validates: Requirements [X.Y, Z.W]**

[Repeat for each property derived from requirements]

## Error Handling

### Error Categories

[N]. **[Error Category Name]**
   - [Error scenario 1]
   - [Error scenario 2]
   - Response: [HTTP status code or error handling approach]

[Repeat for each error category]

### Error Response Format

```[language]
[Error response structure in the specified technology]
```

### Error Handling Strategy

- **[Strategy 1]**: [Description]
- **[Strategy 2]**: [Description]
...

## Testing Strategy

### Unit Testing

[Description of unit testing approach]

- **[Component 1]**: [What to test]
- **[Component 2]**: [What to test]
...

Example unit tests:
- [Test description 1]
- [Test description 2]
...

### Property-Based Testing

[Description of property-based testing approach using appropriate framework for the tech stack]

**Configuration**:
- Each property test should run a minimum of [N] iterations (specify exact number: default 100, use higher for critical/complex properties)
- Each test must be tagged with a comment referencing the design document property
- Tag format: `[comment syntax] Feature: [feature-name], Property {number}: {property_text}`

**Property Test Coverage**:

Each correctness property listed above will be implemented as a property-based test:

[N]. **Property [N] ([Name])**: [Test description]

[Repeat for all properties]

### Integration Testing

[Description of integration testing approach]

- [Integration test scenario 1]
- [Integration test scenario 2]
...

### Test Data Generation

[Description of how to generate test data for the specified tech stack]

```[language]
[Example test data generators]
```

### Testing Tools

- **Unit Testing**: [Framework for tech stack]
- **Property-Based Testing**: [Framework for tech stack]
- **Integration Testing**: [Framework for tech stack]
- **[Other category]**: [Framework for tech stack]
...

### Continuous Testing

- [Testing phase 1]: [When to run]
- [Testing phase 2]: [When to run]
...
```

## Guidelines

### 1. Overview Section
- Provide a high-level description of the system architecture (2-4 paragraphs)
- Mention the chosen technology stack and why it's suitable
- List 3-5 core design principles that guide the architecture
- Examples of design principles:
  - Real-time synchronization
  - Concurrency control
  - User experience focus
  - Scalability
  - Security
  - Performance
  - Maintainability

### 2. Architecture Section

#### Architectural Pattern
- Clearly state the architectural pattern (e.g., 3-tier, microservices, hexagonal, etc.)
- Explain how layers/components interact

#### Mermaid Diagram
- Use `graph TB` (top-to-bottom) or `graph LR` (left-to-right)
- Group related components in `subgraph` blocks
- Show clear dependencies with arrows
- Label all components clearly
- Keep it at the right level of abstraction (not too detailed, not too vague)

#### Technology Stack
- Organize by category (Frontend, Backend, Database, Authentication, Deployment, etc.)
- List specific technologies, frameworks, and versions when relevant
- Include supporting libraries and tools

### 3. Components and Interfaces Section

For each major module identified from requirements:

#### Module Identification
Look at the requirements and identify logical groupings:
- Authentication & Authorization module
- Core business logic modules (one per major entity or feature)
- Validation module
- Data access/persistence module
- UI/Presentation modules

#### Interface Definition
- Use the syntax appropriate for the specified technology stack
- TypeScript/JavaScript: `interface`, `type`, `class`
- Python: `Protocol`, `dataclass`, `TypedDict`
- Java: `interface`, `class`
- Go: `type`, `interface`, `struct`
- Etc.

#### Interface Contents
For each module, define:
- Service interfaces with method signatures
- Data Transfer Objects (DTOs)
- Request/Response types
- Configuration types
- Utility types

#### Naming Conventions
- Follow the idioms of the chosen language/framework
- Use clear, descriptive names
- Be consistent across all interfaces

### 4. Data Models Section

#### Entity Models
For each entity identified in requirements:
- Define the complete data structure
- Include all fields with appropriate types
- Add timestamps (createdAt, updatedAt) where appropriate
- Include relationships/foreign keys
- Use the type system of the chosen technology

#### Database Schema
- Write schema in the appropriate database language (SQL, NoSQL query language, etc.)
- Include:
  - Table/collection definitions
  - Primary keys
  - Foreign keys and relationships
  - Indexes for performance
  - Constraints (unique, not null, default values, etc.)
  - Appropriate data types for the chosen database

### 5. Correctness Properties Section

#### Property Identification
For each requirement (or group of related requirements), identify what property must hold true:

- **Data persistence properties**: "For any X created, querying should return X"
- **State transition properties**: "For any valid state change, the new state should reflect the change"
- **Constraint properties**: "For any operation, constraints should be enforced"
- **Consistency properties**: "For any update, related data should remain consistent"
- **Access control properties**: "For any protected operation, authorization should be verified"

#### Property Format
```
### Property [N]: [Descriptive name]
*For any* [scope/domain], [statement that should always be true].
**Validates: Requirements [list of requirement numbers]**
```

#### Coverage
- Create at least one property for each requirement
- Group related requirements under a single property when logical
- Ensure every acceptance criterion is covered by at least one property

### 6. Error Handling Section

#### Error Categories
Common categories to consider:
- Validation Errors (400)
- Authentication Errors (401)
- Authorization Errors (403)
- Not Found Errors (404)
- Conflict Errors (409)
- Server Errors (500)
- Rate Limiting (429)
- etc.

#### Error Response Format
- Define a standard error response structure for the tech stack
- Include: error code, message, optional details
- Use appropriate type definitions

#### Error Handling Strategy
- Client-side validation approach
- Server-side validation approach
- Transaction management strategy
- Retry logic for transient failures
- Logging and monitoring approach
- User feedback strategy

### 7. Testing Strategy Section

#### Unit Testing
- List what will be tested at the unit level
- Identify critical components that need unit tests
- Provide examples of unit test scenarios
- Suggest appropriate framework for the tech stack

#### Property-Based Testing
This is **critical** and must be comprehensive:

**Framework Selection**:
- JavaScript/TypeScript: `fast-check`
- Python: `hypothesis`
- Java: `jqwik` or `junit-quickcheck`
- Scala: `ScalaCheck`
- Haskell: `QuickCheck`
- Go: `gopter` or `rapid`
- Rust: `quickcheck` or `proptest`
- C#: `FsCheck`

**Configuration**:
- Specify minimum iterations for property tests:
  - **Default: 100 iterations** (sufficient for most properties)
  - Use 200-500 iterations for complex or critical properties only
  - Document the rationale if using more than 100 iterations
- Define tagging/commenting convention for traceability
- Adapt comment syntax to the language (e.g., `//` for C-style, `#` for Python, etc.)

**Test Coverage Mapping**:
- List each correctness property
- Describe how it will be tested with property-based testing
- Explain what will be generated (random inputs)
- Explain what will be verified (invariants)

#### Integration Testing
- Describe end-to-end workflows to test
- List critical integration points
- Suggest appropriate framework for the tech stack

#### Test Data Generation
- Provide examples of data generators for the tech stack
- Show how to generate random valid data
- Show how to generate edge cases
- Use the property-based testing framework's generators

#### Testing Tools
- List specific tools and frameworks for each testing category
- Ensure they're appropriate for the chosen tech stack
- Include additional tools (mocking, API testing, database testing, etc.)

#### Continuous Testing
- Define when each type of test runs
- Suggest CI/CD integration points
- Mention coverage goals if appropriate

### 8. Design Decisions

When making design choices:

#### Match Technology Stack
- If TypeScript/JavaScript: Use TypeScript interfaces, Next.js patterns if specified, etc.
- If Python: Use Python type hints, dataclasses, Pydantic models if applicable, etc.
- If Java: Use Java interfaces, Spring patterns if specified, etc.
- If Go: Use Go interfaces, structs, idiomatic Go patterns, etc.

#### Follow Language Idioms
- Use naming conventions of the language (camelCase, snake_case, PascalCase as appropriate)
- Use standard library patterns and types
- Follow framework conventions if a framework is specified

#### Be Consistent
- Use the same patterns throughout the document
- Use the same naming conventions
- Use the same code style

### 9. Completeness Checklist

Before finalizing, verify:
- [ ] Overview clearly explains the system and design principles
- [ ] Architecture diagram is clear and shows all major components
- [ ] Technology stack matches the provided information
- [ ] All major components from requirements have corresponding modules
- [ ] All interfaces are defined with appropriate types for the tech stack
- [ ] All entities from requirements have data models
- [ ] Database schema includes all tables/collections, keys, and indexes
- [ ] Every requirement is covered by at least one correctness property
- [ ] All error scenarios from requirements are included in error handling
- [ ] Property-based testing section includes all properties with test descriptions
- [ ] Testing tools are appropriate for the chosen tech stack
- [ ] Code examples use correct syntax for the language/framework

### 10. Common Architectural Patterns

Choose based on system complexity and requirements:

- **Layered (N-tier)**: Presentation, Business Logic, Data Access layers
- **Microservices**: Independent services with clear boundaries
- **Hexagonal (Ports and Adapters)**: Core logic isolated from external dependencies
- **Event-Driven**: Components communicate via events
- **CQRS**: Separate read and write operations
- **Serverless**: Function-based architecture

### 11. Mermaid Diagram Examples

**3-Tier Architecture:**
```mermaid
graph TB
    subgraph "Presentation Layer"
        UI[UI Components]
    end

    subgraph "Application Layer"
        API[API/Services]
    end

    subgraph "Data Layer"
        DB[(Database)]
    end

    UI --> API
    API --> DB
```

**Microservices:**
```mermaid
graph LR
    Client[Client]
    Gateway[API Gateway]
    Service1[Service 1]
    Service2[Service 2]
    DB1[(DB 1)]
    DB2[(DB 2)]

    Client --> Gateway
    Gateway --> Service1
    Gateway --> Service2
    Service1 --> DB1
    Service2 --> DB2
```

Adapt to your specific system architecture.

## Important Notes
- This document bridges requirements (WHAT) and implementation (HOW)
- Focus on architectural decisions, not low-level implementation details
- Ensure traceability: every design decision should map back to requirements
- Correctness properties are critical - they drive property-based testing
- Use the actual technology stack provided, not generic pseudo-code
- Maintain language/framework idioms and conventions throughout

## Example Mapping

**From requirements.md:**
```markdown
### Requirement 2
**User Story:** As a User, I want to create a reservation for an available meeting room, so that I can secure a space for my meeting.

#### Acceptance Criteria
1. WHEN a User selects an available time slot, THEN the System SHALL display a reservation form
2. WHEN a User submits a reservation request, THEN the System SHALL validate that the time slot is still available
3. WHEN a reservation is valid, THEN the System SHALL create the reservation and update the dashboard
```

**To design.md (TypeScript example):**
```typescript
### 3. Reservation Management Module

**책임**: 예약 생성, 수정, 취소 및 조회

**인터페이스**:
interface ReservationService {
  createReservation(reservation: CreateReservationDto): Promise<Reservation>;
  checkAvailability(roomId: string, timeSlot: TimeSlot): Promise<boolean>;
}

interface CreateReservationDto {
  userId: string;
  roomId: string;
  startTime: Date;
  endTime: Date;
}

### Correctness Properties

### Property 3: Time slot availability validation
*For any* reservation creation request, the system should validate that the requested time slot has no overlapping active reservations before allowing the operation.
**Validates: Requirements 2.2**

### Property-Based Testing
3. **Property 3 (Availability validation)**: Generate random time slots, verify overlap detection logic correctly identifies conflicts
```

## Now Generate

Please provide:
1. The complete `requirements.md` content
2. The technology stack information (language/framework, database, etc.)

And I will generate a comprehensive `design.md` document following this template.

**Important Requirements:**
- The generated document must be written in **Korean (한글)**
- Code examples, interfaces, and technical syntax should remain in the programming language
- Comments and descriptions should be in Korean
- Save the generated file as `.kiro/specs/design.md`
