---
name: le:plan
description: Create a clear, step-by-step implementation plan based on a brainstorm requirements document. Saves to docs/plans/ and updates docs/features/.
argument-hint: "[feature name or requirements doc path]"
---

# Implementation Planning

Use this skill to turn a brainstormed requirements document (from `docs/brainstorms/`) into a concrete, executable, step-by-step technical implementation plan.

This skill runs strictly in the main chat context.

## Plan Stage Constraints
- **Mandatory Order**: The plan stage **must** follow the brainstorm stage. Do not execute this skill without a finalized requirements document in `docs/brainstorms/`.
- **Strict Rule: Technical Elicitation ONLY**: During this planning phase, ask questions **only** about technical details, databases, libraries, tools, frameworks, and architecture.
- Do NOT modify the product rules, scope, or user flows established in the requirements document. If a technical challenge conflicts with the requirements, discuss it with the user as a technical trade-off.

---

## Action Steps

### Step 1: Read Requirements Context
- Locate and read the corresponding requirements document in `docs/brainstorms/YYYY-MM-DD-<feature-name>-requirements.md`.
- If no requirements document exists, tell the user that `/le:brainstorm` must be completed first.

### Step 2: Technical Elicitation (One Question at a Time)
- Ask the user clarifying questions regarding:
  - Technology stack, frameworks, and library versions.
  - Database schema, table structures, migrations, or caching.
  - Directory layouts, file names, naming conventions, and exports.
  - Integration checkpoints and HTTP/API endpoint structures.
- **Rule**: Ask exactly **one question per turn** to keep the technical dialogue structured.

### Step 3: Write Implementation Plan Document
Save the generated plan to:
`docs/plans/YYYY-MM-DD-<feature-name>-plan.md`

#### Plan Document Template:
```markdown
# Implementation Plan: [Feature Name]
Date: YYYY-MM-DD
Requirements: docs/brainstorms/YYYY-MM-DD-[feature-name]-requirements.md

## 1. Technical Architecture & Decisions
- **Stack & Libraries**: [Frameworks, databases, external tools used.]
- **Database Schema / State**: [Table structures or key data models.]
- **Endpoints / API Design**: [HTTP paths, signatures, payloads.]

## 2. Proposed Changes
Break down files to modify/create:

### [Component / Layer Name]
#### [MODIFY/NEW] `[file path]`
- [Specific code-level change description]

## 3. Verification Plan
### Automated Tests
- [Exact unit/integration tests to run or write, matching docs/Testing.md]

### Manual Verification
- [Verification steps]
```

### Step 4: Automate Logging (MANDATORY)
Immediately after saving the plan, **automatically execute the logging logic (`le:log`)** to update `docs/features/<feature-name>-log.md`:
- Record that the implementation plan was created in `docs/plans/`.
- Document any technical constraints, trade-offs, or deferred items.

Provide the user with clickable links to both the plan file and the updated feature log file.
