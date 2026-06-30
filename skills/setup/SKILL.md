---
name: le:setup
description: Run this to set up a new project's quality-control guidelines and directory structure (creates docs/brainstorms/, docs/plans/, docs/features/, docs/solutions/, Testing.md, Security.md, DefinitionOfDone.md, Arch.md, and CodeStyle.md).
---

# Setup Project Quality and Guidelines

Use this skill to bootstrap a new software project with standard quality, testing, security, and styling guidelines.

This skill runs strictly in the main chat context.

## Action Steps

1. **Verify or Create Directory Structure**:
   - Ensure the following directories exist under `docs/`:
     - `docs/brainstorms/` (for requirements documents from `le:brainstorm`)
     - `docs/plans/` (for implementation plans from `le:plan`)
     - `docs/features/` (for per-feature agent logs from `le:log`)
     - `docs/solutions/` (for architecture patterns and project solutions)

2. **Generate Quality templates**:
   Write the following standard files if they do not already exist in the project's root or `docs/` directory. If they exist, review them with the user.

---

### File 1: [NEW] `docs/Testing.md`

Generate this standard structure:

```markdown
# Testing Guidelines & Strategy

This document outlines the testing standards for this codebase.

## 1. Core Testing Strategy
- **Primary Focus**: High unit test coverage (target: 80% to 90% of new or modified code).
- **Secondary Focus**: Integration tests to verify database interactions, API endpoints, or cross-service behaviors where valuable.
- **Speed & Isolation**: Unit tests must run fast. Mock heavy resources to avoid slow test suites.

## 2. Mocking & Isolation Rules
- **Mocking is highly encouraged**: Mock database adapters, repositories, external services, and complex helper modules in Unit tests.
- **Separate Testing of Layers**: Since repositories, services, controllers, and helpers have their own dedicated test files, do not test them together in Unit tests. Mock the dependency layer to test the current module in isolation.
- **Mocking Databases**: Use mocks/stubs for database layers in unit tests. Real databases (e.g., local SQLite or Postgres in Docker) should be reserved for integration tests.

## 3. Debugging & Regression Testing (MANDATORY RULE)
- **Turn bugs into tests**: Whenever a bug is found and debugged, you **MUST** write a test that reproduces the bug before fixing it.
- **Verification**: The test must fail when the bug is present, and pass once the bug is resolved.
- **Purpose**: Prevents regressions, locks in debugging findings, and stops future token waste on identical debug investigations.

## 4. Test Coverage Requirements
Every test suite must include:
- **Positive Tests**: Verifying successful flows, valid inputs, and expected outcomes (happy path).
- **Negative Tests**: Verifying error handling, invalid inputs, exception catching, and failure paths.
- **Corner Cases**: Cover boundary conditions, empty values, null/undefined, overflow, and extreme inputs.

## 5. Coding Standards
- **Naming Pattern**: Use `should [expected behavior] when [scenario/inputs]` (e.g., `should return token when credentials are valid`).
- **AAA Structure**: Structure test logic clearly into:
  - **Arrange**: Set up mocks, inputs, and test state.
  - **Act**: Execute the function/method under test.
  - **Assert**: Verify outputs, state changes, and mock calls.
```

---

### File 2: [NEW] `docs/DefinitionOfDone.md`

Generate this checklist:

```markdown
# Definition of Done (DoD)

A task is not considered completed until it satisfies all requirements in this checklist.

## 1. Code Quality
- [ ] Code compiles and builds successfully without errors.
- [ ] Linter is run (adhering to project-specific rules and strictness).
- [ ] No dead code, debug statements (`console.log`, `print`, `debugger`), or temporary files are left.
- [ ] No unexpected `TODO` or `TBD` placeholders are left in the modified files.

## 2. Git Workflow
- [ ] Commits are formatted strictly using **Conventional Commits** (e.g., `feat: ...`, `fix: ...`, `docs: ...`).
- [ ] The branch is fully updated (merged or rebased) with the target development branch (`dev` or `main`) before completing.

## 3. Testing & Bug Fixing
- [ ] Unit tests are written for all new and modified code.
- [ ] Unit test coverage of new/modified code is between **80% and 90%**.
- [ ] Positive, negative, and edge cases are covered.
- [ ] **Regression Check**: Any bug fixed during this task is covered by an automated test that fails before the fix and passes after.
- [ ] All automated tests pass successfully.

## 4. Documentation & Tracking
- [ ] Code comments are added to public interfaces, complex logic, and helper scripts.
- [ ] System architecture doc (`docs/Arch.md`) is updated if structural changes were made.
- [ ] The feature log file (`docs/features/<feature-name>-log.md`) is created or updated.

## 5. Review
- [ ] The code-review subagent (`le:code-review`) has been executed.
- [ ] All Critical and Important issues found by the reviewer have been resolved.
```

---

### File 3: [NEW] `docs/Security.md`

Generate this checklist:

```markdown
# Security Standards & Guidelines

Security is a primary requirement. Follow these rules to protect our applications and data.

## 1. Secrets Management
- **Zero Hardcoded Secrets**: Never write API keys, passwords, private keys, database credentials, or tokens in the codebase.
- **Environment Variables**: Load all secrets through environment variables or secure vault configuration.
- **Gitignore Config**: Ensure all `.env` files and local configurations are strictly added to `.gitignore`.

## 2. Input Validation & Sanitization
- **Strict Schema Validation**: Validate all incoming parameters (body, headers, query, route arguments) against strict schemas (e.g., Zod, Pydantic, JSON Schema).
- **Prevent SQL Injection**: Use ORMs or parameterized queries. Never concatenate variables directly into SQL queries.
- **Prevent XSS**: Sanitize and escape all user-generated HTML/XML content before rendering.

## 3. Authorization & IDOR Prevention
- **Access Control**: Enforce authorization checks on all restricted endpoints.
- **Insecure Direct Object Reference (IDOR)**: Always check ownership. Ensure the currently logged-in user has permission to view/modify the requested resource ID (e.g., check `userId == resource.ownerId`).

## 4. Dependency Safety
- Run a dependency vulnerability check (e.g., `npm audit` or language equivalent).
- Report any vulnerabilities to the user. (Note: Vulnerabilities will be shown as warnings and do not block task completion, but they must be documented).

## 5. Sensitive Data & Log Masking
- Never write credentials, full credit card details, passwords, or PII (Personally Identifiable Information) in application logs.
- Mask sensitive values if logging is required.

## 6. Static Analysis (SAST)
- Code security auditing is performed automatically by the Code Reviewer / Security Auditor subagents during the review phase.
```

---

### File 4: [NEW] `docs/CodeStyle.md`

Create a template file detailing code styling rules (indentation, naming casing, file sizing, comments style) to be customized by the user.

### File 5: [NEW] `docs/Arch.md`

Create a template file describing the architectural patterns (MVC, Hexagonal, Clean, layered), main dependencies, directory layouts, and data flow.
