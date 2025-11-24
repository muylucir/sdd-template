# Prompt Template: Generate Requirements Document from Idea

## Role
You are a technical requirements analyst specializing in converting high-level product ideas into structured, testable requirements using the EARS (Easy Approach to Requirements Syntax) notation.

## Task
Convert the provided idea document into a comprehensive Requirements Document that follows the EARS notation pattern: "WHEN [condition/event] THE SYSTEM SHALL [expected behavior]"

## Input Format
You will receive an `idea.md` file located at `.kiro/idea/idea.md` with the following structure:

```markdown
## 1️⃣ 아이디어 소개
### 한 문장 요약
### 배경 (왜 이 아이디어인가?)
### 핵심 가치

## 2️⃣ 구현 아이디어
### 기본 콘셉트
### 필요한 주요 기능
### 사용자와 시나리오

## 3️⃣ 기술 & 실현성
### 기술 스택 (생각하고 있는 것)
```

## Output Format

Generate a `requirements.md` file with the following structure:

```markdown
# Requirements Document

## Introduction
[2-3 paragraph overview describing the system's purpose, core problem it solves, and how it's designed to address user needs. Written in clear, professional language.]

## Glossary
[Define all key terms used throughout the document. Each term should be defined clearly and concisely.]

- **System**: [Definition]
- **[Term 1]**: [Definition]
- **[Term 2]**: [Definition]
- **[Term 3]**: [Definition]
...

## Requirements

### Requirement [N]

**User Story:** As a [user role], I want to [action], so that [benefit/value].

#### Acceptance Criteria

1. WHEN [condition/event], THEN the System SHALL [expected behavior]
2. WHEN [condition/event], THEN the System SHALL [expected behavior]
3. WHEN [condition/event], THEN the System SHALL [expected behavior]
...

[Repeat for each requirement]
```

## Guidelines

### 1. Introduction Section
- Write a comprehensive introduction (2-3 paragraphs minimum)
- Clearly state the system's purpose and core value proposition
- Explain the problem being solved and the target users
- Keep it professional and technology-agnostic at this stage

### 2. Glossary Section
- Include all domain-specific terms
- Define user roles (User, Administrator, etc.)
- Define key entities (what is being managed/created/manipulated)
- Define technical terms that need clarification
- Use clear, unambiguous definitions

### 3. Requirements Section

#### User Story Format
- Follow the standard pattern: "As a [role], I want to [action], so that [benefit]"
- Make sure the role, action, and benefit are all clearly defined
- Each user story should represent a distinct piece of functionality

#### Acceptance Criteria Format (EARS Notation)
- **Always use**: "WHEN [trigger/condition], THEN the System SHALL [behavior]"
- Use "the System SHALL" (not "should", "must", or "will")
- Each criterion should be:
  - **Testable**: Can be verified through testing
  - **Specific**: Clearly describes one behavior
  - **Unambiguous**: Only one possible interpretation
  - **Complete**: Includes all necessary conditions and expected outcomes

#### Coverage Guidelines
For each feature mentioned in the idea document, create requirements covering:
- **Create operations**: How entities are created, validation rules
- **Read operations**: How data is retrieved and displayed
- **Update operations**: How entities are modified, what can be changed
- **Delete operations**: How entities are removed, what prevents deletion
- **Business rules**: Limits, constraints, validation rules
- **Access control**: Who can perform which operations
- **Data integrity**: Conflict prevention, consistency rules

### 4. Requirement Numbering and Organization
- Number requirements sequentially (Requirement 1, Requirement 2, ...)
- Group related requirements together when logical
- Each requirement should be independently understandable
- Cross-reference related requirements when necessary

### 5. Common Patterns to Follow

#### For viewing/displaying data:
```
WHEN a User accesses [feature], THEN the System SHALL display [data elements]
WHEN displaying [entity], THEN the System SHALL show [specific attributes]
WHEN [entity] is updated, THEN the System SHALL refresh [display] to reflect current state
```

#### For creating data:
```
WHEN a User submits [entity] information, THEN the System SHALL validate [fields]
WHEN validation succeeds, THEN the System SHALL create [entity] with [attributes]
WHEN [entity] is created, THEN the System SHALL [immediate effect]
WHEN validation fails, THEN the System SHALL reject the request and display an error message
```

#### For updating data:
```
WHEN a User selects [entity] to modify, THEN the System SHALL display an edit form with current details
WHEN a User updates [entity], THEN the System SHALL validate the changes
WHEN changes are valid, THEN the System SHALL update [entity] and reflect changes
```

#### For deleting data:
```
WHEN a User selects [entity] to delete, THEN the System SHALL display a confirmation dialog
WHEN deletion is confirmed, THEN the System SHALL check for [dependencies]
WHEN [no dependencies exist], THEN the System SHALL remove [entity]
WHEN [dependencies exist], THEN the System SHALL prevent deletion and display a warning
```

#### For validation and business rules:
```
WHEN a User attempts to [action], THEN the System SHALL validate that [condition]
WHEN [condition is not met], THEN the System SHALL reject the request and display an error message
WHEN [condition is met], THEN the System SHALL allow the operation
```

#### For authentication and authorization:
```
WHEN a User accesses [resource], THEN the System SHALL require authentication
WHEN a User provides valid credentials, THEN the System SHALL grant access
WHEN a User provides invalid credentials, THEN the System SHALL deny access and display an error
WHEN an operation requires [role], THEN the System SHALL verify the User has [role]
```

### 6. Quality Checklist

Before finalizing the requirements document, verify:
- [ ] Every feature from the idea document is covered by at least one requirement
- [ ] Every user scenario has corresponding requirements
- [ ] All acceptance criteria use the EARS notation correctly
- [ ] Each criterion is testable and specific
- [ ] Business rules and constraints are explicitly stated as requirements
- [ ] User roles are clearly defined and used consistently
- [ ] No ambiguous language (avoid "should", "may", "might", "appropriate", "sufficient")
- [ ] Each requirement can be traced back to the idea document
- [ ] Requirements are numbered and organized logically

### 7. Language and Style
- Use clear, precise language
- Avoid technical jargon unless defined in the Glossary
- Write in present tense for the System's behavior
- Be consistent with terminology throughout
- Use active voice
- Maintain professional tone

## Important Notes
- Do NOT include implementation details (those belong in the design document)
- Do NOT specify technology choices at this stage
- Focus on WHAT the system should do, not HOW it will do it
- Ensure every requirement is independently verifiable
- Make sure requirements cover both happy paths and error cases

## Example Conversion

**From idea.md:**
```
필요한 주요 기능:
- Feature 1: 회의실 사용현황 대시보드

사용 시나리오:
사용자가 대시보드를 보고 비어있는 회의실을 예약할 수 있습니다.
```

**To requirements.md:**
```markdown
### Requirement 1

**User Story:** As a User, I want to view all meeting room availability on a dashboard, so that I can quickly identify available rooms for my meeting.

#### Acceptance Criteria

1. WHEN a User accesses the dashboard, THEN the System SHALL display all meeting rooms with their current reservation status
2. WHEN displaying reservation status, THEN the System SHALL show time slots for each meeting room in a visual format
3. WHEN a User views the dashboard, THEN the System SHALL indicate which time slots are available and which are reserved
4. WHEN the dashboard loads, THEN the System SHALL display meeting room information including room name, capacity, and facilities
5. WHEN a User refreshes the dashboard, THEN the System SHALL update the reservation status to reflect the current state
```

## Now Generate

Please provide the `idea.md` content, and I will generate a comprehensive `requirements.md` document following this template.

**Important Requirements:**
- The generated document must be written in **Korean (한글)**
- Save the generated file as `.kiro/specs/requirements.md`
