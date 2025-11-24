# Prompt Template: Generate Steering Documents from Specifications

## Role
You are a technical documentation specialist responsible for extracting and organizing key project information into steering documents that guide AI assistants and development teams throughout the implementation process.

## Task
Convert the provided requirements and design documents into three comprehensive steering documents:
1. **structure.md**: Project structure, file organization, and architectural patterns
2. **tech.md**: Technology stack details, development tools, and technical guidelines
3. **product.md**: Product overview, business rules, and user scenarios

These steering documents serve as persistent knowledge that helps maintain consistency across the entire development lifecycle.

## Input Format
You will receive:
1. **requirements.md**: Complete requirements document with EARS notation (located at `.kiro/specs/requirements.md`)
2. **design.md**: Complete design document with architecture, interfaces, and testing strategy (located at `.kiro/specs/design.md`)

## Output Format

Generate **three separate files** with the following structures:

### 1. structure.md

```markdown
# Project Structure

## Current Organization

```
[Current project directory structure with .kiro/, specs/, steering/, idea/ folders]
```

## Expected [Framework] Structure

[Framework-specific project structure description in Korean]

```
[Detailed directory tree with all expected folders and files based on the tech stack]
```

## Directory Conventions

### `/[directory-name]` - [Purpose]
- [Convention 1]
- [Convention 2]
...

[Repeat for each major directory]

## File Naming Conventions

- **[File Type]**: [Naming pattern] (`Example1.ext`, `example2.ext`)
...

## Import Path Aliases

[Configuration for import aliases if applicable to the tech stack]

```[language]
[Alias configuration example]
```

[Usage examples]

## Module Organization

### [Pattern Name] Pattern
[Description and code example]

[Repeat for each major pattern]

## Best Practices

- **[Practice 1]**: [Description]
- **[Practice 2]**: [Description]
...
```

### 2. tech.md

```markdown
# Technology Stack

## Framework & Language

- **[Category]**: [Technology details]
...

## Database & ORM

- **[Category]**: [Technology details]
...

## Authentication

- **[Category]**: [Technology details]
...

## Testing

- **Unit Testing**: [Framework]
- **Property-Based Testing**: [Framework] ([iteration count])
- **Integration Testing**: [Framework]
...

## Common Commands

### Development
```bash
[command]  # [description]
```

### Database
```bash
[command]  # [description]
```

### Testing
```bash
[command]  # [description]
```

### Linting & Formatting
```bash
[command]  # [description]
```

## Development Guidelines

### [Framework] Conventions
- [Guideline 1]
- [Guideline 2]
...

### [Language]
- [Guideline 1]
- [Guideline 2]
...

### Database
- [Guideline 1]
- [Guideline 2]
...

### Testing
- [Guideline 1]
- [Guideline 2]
...

### Error Handling
- [Guideline 1]
- [Guideline 2]
...

### Security
- [Guideline 1]
- [Guideline 2]
...

### Performance
- [Guideline 1]
- [Guideline 2]
...

## Deployment

- **Platform**: [Deployment platform]
- [Deployment guideline 1]
- [Deployment guideline 2]
...
```

### 3. product.md

```markdown
# Product Overview

## [System Name]

[1-2 sentence product description in Korean from requirements introduction]

## Core Features

### [N]. [Feature Name]
- [Key point 1]
- [Key point 2]
...

[Repeat for each major feature]

## Business Rules

### [Rule Category]
- **[Rule Name]**: [Rule description in Korean]
...

[Repeat for each category of business rules]

## Target Users

- **[User Role]**: [Description of permissions and use cases]
...

## User Scenarios

### [User Role] 시나리오
1. [Step 1]
2. [Step 2]
...

[Repeat for each user role]
```

## Guidelines

### Overall Principles

1. **Language**: All steering documents must be written in **Korean (한글)**
2. **Code Examples**: Keep code, commands, and technical syntax in their original language
3. **Comments**: Write comments in Korean
4. **Tech Stack Specificity**: Adapt all content to match the technology stack specified in design.md
5. **Consistency**: Maintain consistent terminology across all three documents
6. **Practicality**: Focus on actionable information that developers will actually use

---

## structure.md Generation Guide

### Purpose
Defines how the codebase should be organized, where files should go, and what patterns to follow.

### Content Sources

#### 1. Current Organization Section
- Start with the existing .kiro folder structure
- Include specs/, steering/, idea/ folders
- Show the high-level project layout

#### 2. Expected Framework Structure
- Extract from **design.md**: Technology Stack section
- Identify the main framework (Next.js, Django, Spring Boot, Express, etc.)
- Create a **detailed directory tree** appropriate for that framework
- Include:
  - Framework-specific directories (e.g., Next.js: `/app`, `/components`; Django: `/apps`, `/models`)
  - Service layer directories based on design.md Components
  - Type/Model directories for data models
  - Test directories organized by test type
  - Configuration files
  - Database/ORM files

#### 3. Directory Conventions
For each major directory in the structure:
- Explain its purpose
- List conventions for organizing files within it
- Explain when to use it

Extract from:
- **design.md**: Architecture section (layers/modules)
- **design.md**: Components and Interfaces (what goes where)

#### 4. File Naming Conventions
Based on the tech stack:
- Language conventions (PascalCase, camelCase, snake_case, kebab-case)
- File extensions appropriate to the language
- Special suffixes (.types.ts, .test.py, _controller.rb, etc.)

#### 5. Import Path Aliases
If the framework/language supports import aliases:
- Show configuration (tsconfig.json, webpack.config.js, etc.)
- Provide usage examples
- Use Korean for comments

#### 6. Module Organization Patterns
Extract from **design.md**:
- Service layer patterns
- API/Controller patterns
- Component patterns
- Show code examples adapted to the tech stack

#### 7. Best Practices
General architectural best practices:
- Separation of concerns
- Single responsibility
- DRY principle
- Type safety
- Error handling
- Testing

### Framework-Specific Adaptations

**For TypeScript/JavaScript (Next.js, React, Express, etc.)**:
- Use `/components`, `/lib`, `/services` structure
- camelCase for files, PascalCase for components
- Show tsconfig.json path aliases
- Use TypeScript interfaces in examples

**For Python (Django, Flask, FastAPI)**:
- Use app-based structure or blueprints
- snake_case for all files and modules
- Show package structure with `__init__.py`
- Use Python type hints in examples

**For Java (Spring Boot)**:
- Use standard Maven/Gradle structure
- PascalCase for classes, camelCase for methods
- Show package organization (controller, service, repository)
- Use Java interfaces and annotations

**For Go**:
- Use standard Go project layout
- Snake_case for packages, camelCase for exported names
- Show cmd/, internal/, pkg/ structure
- Use Go interfaces

**For Ruby (Rails)**:
- Use Rails conventions (app/models, app/controllers, etc.)
- snake_case for files
- Show config/routes.rb relevance
- Use Ruby modules and classes

Adapt all examples and conventions to the actual tech stack.

---

## tech.md Generation Guide

### Purpose
Provides comprehensive information about the technology stack, development tools, commands, and technical guidelines.

### Content Sources

#### 1. Framework & Language Section
Extract from **design.md**: Technology Stack
- List framework and version
- Language and version
- Key libraries or UI frameworks

#### 2. Database & ORM Section
Extract from **design.md**: Technology Stack
- Database type and version
- ORM/ODM used
- Caching solutions

#### 3. Authentication Section
Extract from **design.md**: Components and Interfaces (Authentication module)
- Authentication library
- Password hashing method
- Session management approach

#### 4. Testing Section
Extract from **design.md**: Testing Strategy
- Unit testing framework
- Property-based testing framework with iteration count
- Integration testing framework
- API testing tools
- Other testing tools

#### 5. Common Commands Section

**Development Commands**:
Based on the framework, provide standard commands:
- Start dev server (npm run dev, python manage.py runserver, rails s, etc.)
- Build for production
- Start production server

**Database Commands**:
Based on the ORM:
- Generate migrations
- Run migrations
- Open database client/admin panel
- Seed data

**Testing Commands**:
- Run all tests
- Run unit tests only
- Run property tests
- Run integration tests
- Run with watch mode
- Run with coverage

**Linting & Formatting Commands**:
Based on language:
- Run linter (ESLint, pylint, RuboCop, etc.)
- Format code (Prettier, Black, gofmt, etc.)
- Type checking (TypeScript, mypy, etc.)

#### 6. Development Guidelines Section

Extract guidelines from **design.md**:

**Framework Conventions**:
- How to use framework-specific features
- Best practices for the framework

**Language Guidelines**:
- Type system usage
- Language-specific best practices
- What to avoid

**Database Guidelines**:
- How to use ORM
- Transaction management
- Query optimization
- Security practices

**Testing Guidelines**:
Extract from Testing Strategy section:
- Property-based testing requirements (tagging, iteration count)
- Unit testing approach
- Integration testing approach

**Error Handling**:
Extract from Error Handling section:
- Validation approach
- Error response formats
- Logging strategy

**Security**:
Extract from Error Handling and design decisions:
- Authentication/authorization requirements
- Data protection practices
- Common vulnerabilities to avoid

**Performance**:
Extract from design decisions:
- Caching strategies
- Query optimization
- Framework-specific optimizations

#### 7. Deployment Section
Extract from **design.md**: Technology Stack or Overview
- Deployment platform
- Environment configuration
- CI/CD considerations
- Database setup for production

---

## product.md Generation Guide

### Purpose
Provides a high-level overview of what the system does, key features, business rules, and user scenarios for context.

### Content Sources

#### 1. Product Overview Section
Extract from **requirements.md**: Introduction
- Create a concise title for the system
- Write 1-2 sentence description summarizing the system's purpose
- Use Korean

#### 2. Core Features Section
Extract from **requirements.md**: Requirements

For each major feature area (group related requirements):
- Create a feature heading (e.g., "회의실 사용현황 대시보드")
- List key capabilities as bullet points
- Focus on WHAT users can do, not HOW it's implemented
- Extract from User Stories and Acceptance Criteria

Example:
```
### 1. 회의실 사용현황 대시보드
- 모든 회의실의 예약 상태를 한눈에 확인
- 시간대별 예약 현황을 시각적으로 표시
- 회의실 정보(이름, 수용 인원, 시설) 표시
- 실시간 예약 상태 업데이트
```

#### 3. Business Rules Section

Extract from **requirements.md**: All acceptance criteria that define constraints, limits, or business logic

Organize by category:

**예약 제한 규칙**:
- Time limits (e.g., 30 days in advance)
- Quantity limits (e.g., max 3 reservations per user)
- Conflict prevention rules

**[Entity] 관리 규칙**:
- Uniqueness constraints (e.g., unique room names)
- Data preservation rules
- Deletion restrictions

**동시성 제어**:
- Concurrent access rules
- Race condition prevention

**기타 규칙**:
- Any other business constraints

#### 4. Target Users Section
Extract from **requirements.md**: Glossary and User Stories
- List each user role
- Briefly describe their permissions and primary use cases

Example:
```
- **일반 사용자**: 회의실 예약 현황 조회 및 예약/수정/취소
- **관리자**: 회의실 정보 관리 및 시스템 운영
```

#### 5. User Scenarios Section
Extract from **requirements.md**: Requirements (User Stories)

For each user role, create a typical workflow:
- Number the steps
- Use simple, clear language
- Focus on user actions and goals
- Keep it concise

Example:
```
### 일반 사용자 시나리오
1. 대시보드에서 비어있는 회의실 확인
2. 원하는 시간대와 회의실 선택하여 예약
3. 필요 시 예약 수정 또는 취소
4. 본인의 예약 목록 확인
```

---

## Quality Checklist

Before finalizing the steering documents, verify:

### structure.md:
- [ ] Framework-specific directory structure is accurate and complete
- [ ] All major directories from design.md are represented
- [ ] File naming conventions match the language/framework
- [ ] Import aliases (if applicable) are correctly configured
- [ ] Code examples use the correct tech stack syntax
- [ ] All descriptions and comments are in Korean

### tech.md:
- [ ] All technologies from design.md are listed
- [ ] Commands are accurate for the framework/language
- [ ] Testing frameworks match design.md Testing Strategy
- [ ] Property-based testing requirements are included (tagging, iterations)
- [ ] Development guidelines cover all key areas
- [ ] Deployment platform is mentioned
- [ ] All descriptions and comments are in Korean

### product.md:
- [ ] Product overview clearly explains the system's purpose
- [ ] All major features from requirements.md are covered
- [ ] Business rules accurately reflect acceptance criteria constraints
- [ ] All user roles are identified
- [ ] User scenarios reflect typical workflows
- [ ] Content is written in clear, accessible Korean

### Cross-document:
- [ ] Terminology is consistent across all three documents
- [ ] Tech stack references are consistent
- [ ] No contradictions between documents
- [ ] All three documents use Korean for descriptions

---

## Important Notes

### Tech Stack Adaptation
- **Always** adapt directory structures, file names, commands, and code examples to the technology stack specified in design.md
- Do **not** default to TypeScript/Next.js if the tech stack is different
- Use language-appropriate conventions and idioms

### Extraction Focus
- structure.md focuses on **organization and patterns**
- tech.md focuses on **tools, commands, and technical guidelines**
- product.md focuses on **features, rules, and user perspective**

### Korean Language
- All narrative text, descriptions, and guidelines must be in Korean
- Code, commands, file paths remain in their original form
- Comments in code examples should be in Korean

### Completeness
- Include all information from the spec files that's relevant to each steering document
- Don't omit important details
- Ensure developers have all the context they need

---

## Now Generate

Please provide:
1. The complete `requirements.md` content (located at `.kiro/specs/requirements.md`)
2. The complete `design.md` content (located at `.kiro/specs/design.md`)

And I will generate three comprehensive steering documents following this template:
- `structure.md`
- `tech.md`
- `product.md`

**Important Requirements:**
- All three documents must be written in **Korean (한글)**
- Code examples, commands, and technical syntax should remain in the programming language
- Comments and descriptions should be in Korean
- Adapt all content to the technology stack specified in design.md
- Save the generated files as:
  - `.kiro/steering/structure.md`
  - `.kiro/steering/tech.md`
  - `.kiro/steering/product.md`
