---
name: le:using-le
description: Used when starting any conversation - establishes how to find and use skills, requirements checking, per-feature logs, and code review rules.
---

# Using Lightweight Engineering (le)

Welcome! This toolkit contains highly optimized, token-efficient workflows for developing software in this codebase.

## Core Rules for the Agent

You must follow these rules at all times. They ensure consistency, quality, and context safety across development sessions.

### 1. Link Brainstorming, Planning, and Execution
Before starting to code or implement any feature:
- **Search** for a corresponding requirements document under `docs/brainstorms/YYYY-MM-DD-<feature-name>-requirements.md`.
- **Search** for an implementation plan under `docs/plans/YYYY-MM-DD-<feature-name>-plan.md`.
- **Align** your implementation strictly with the decisions made in those documents. 
- **Rule of Sequence**: You cannot write a plan (`le:plan`) or write code without a finalized requirements document (`le:brainstorm`). 

### 2. Strict Division of Workflow Roles
- **`/le:brainstorm` (Product Logic stage)**: Focuses **exclusively** on the functional requirements, user flows, outcomes, and business edge cases.
  - **Strict Constraint**: Do NOT ask about or define database tables, file names, API designs, frameworks, libraries, or programming languages.
- **`/le:plan` (Technical Design stage)**: Focuses **exclusively** on the implementation details, database schema, file changes, APIs, libraries, and tests.
  - **Strict Constraint**: Inherit product requirements verbatim from the brainstorm document. Do NOT modify the core product logic here.
- **`/le:log` (Logging stage)**: Automatically updates the feature history after brainstorming, planning, and coding tasks.

### 3. Strict Debugging & Regression Testing Rule (MANDATORY)
Whenever you are debugging an issue or fixing a bug:
- **Analyze and reproduce**: Write down the steps and root cause of the bug.
- **Write a Regression Test**: Before marking the bug as fixed, you **MUST** write a Unit/Integration test that reproduces the bug (it must fail before the fix is applied and pass after the fix).
- **Goal**: Lock in the debug findings as an automated test so that the bug never recurs, preventing long debug cycles and wasting tokens in the future.

### 4. Search and Reference Feature Logs
When you are asked to modify, bugfix, extend, or explain an existing feature:
- **Locate and read** the feature's log file at `docs/features/<feature-name>-log.md` before making changes.
- **Verify** what was done, what was **not** done, and the **reasoning** (out of scope, conscious trade-off, by design) before proposing changes.
- Respect conscious trade-offs and out-of-scope markers documented in the log. If a request conflicts with an established trade-off, raise this to the user for clarification.

### 5. Automatic Per-Feature Logging (MANDATORY)
To avoid token bloat and save context window, **never** use a single massive project log. Instead:
- Keep logs localized: **one file per feature** under `docs/features/<feature-name>-log.md`.
- **Automate Logging**: Run or update `le:log` automatically at the end of every workflow (`le:brainstorm`, `le:plan`, and coding/debugging tasks). Do not wait for the user to ask for logging.
- **Mandatory Content**: Always document what was NOT done and why (e.g. designed this way, out of scope, or a conscious trade-off).

### 6. Single-Chat Context (Except Code Review)
- Perform all brainstorming (`le:brainstorm`), planning (`le:plan`), project setups (`le:setup`), and log updates (`le:log`) **directly in the main chat context**.
- Only the **`le:code-review`** skill is allowed to spawn subagents. It will spawn two specialized subagents (Code Quality Reviewer and Security Auditor) concurrently to provide an isolated and expert-level code audit.

---

## Active Skills in this Toolkit

- **`le:setup`**: Prepares project directories (`docs/brainstorms/`, `docs/plans/`, `docs/features/`, `docs/solutions/`) and quality-control markdown files.
- **`le:brainstorm`**: Explores requirements and writes a spec in `docs/brainstorms/`, automatically logging to `docs/features/`.
- **`le:plan`**: Creates a step-by-step implementation plan in `docs/plans/`, automatically logging to `docs/features/`.
- **`le:code-review`**: Spawns concurrent subagents to review logic and security before merging.
- **`le:log`**: Creates or updates a feature's development log in `docs/features/`.
