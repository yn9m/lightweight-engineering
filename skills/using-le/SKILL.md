---
name: le:using-le
description: Used when starting any conversation - establishes the Bug-to-Autotest Guarantee and the Git Commit Self-Documentation workflow.
---

# Lightweight Engineering (le)

Welcome! This is a highly optimized, token-efficient AI-first framework. All decisions and history are kept decentralized.

## Core Rules for the Agent

You must follow these rules at all times.

### 1. Bug-to-Autotest Guarantee (MANDATORY)
Whenever you debug an issue or fix a bug/error in the codebase:
- **Write a Regression Test**: Before marking the task as complete, you **MUST** write an automated test (unit or integration) that reproduces the bug.
- **Verification**: The test must fail when the bug is present, and pass once the fix is applied.
- **Purpose**: Prevents regressions, locks in debugging findings as code, and stops future token waste on identical debug investigations.

### 2. Decentralized Commit Self-Documentation (MANDATORY)
To avoid context bloat and the high token cost of reading/writing separate markdown log files, **do not create log files, PRDs, specs, or plans**. 

Instead, document your progress directly in the **Git commit message**. When you make a commit (or write the commit message for the user), you **MUST** format the commit message using the following template:

```text
[feat/fix/chore]: <short description in Conventional Commits format>

### What was done:
- [relative file path] - [brief description of changes]
- [relative file path] - [brief description of changes]

### What was NOT done & Why (MANDATORY):
- <item omitted/deferred> [By Design: explanation]
- <item omitted/deferred> [Out of Scope: explanation]
- <item omitted/deferred> [Conscious Trade-off: explanation]
```

#### Classification Definitions:
- **By Design**: Core architectural choice to avoid complexity or keep features clean.
- **Out of Scope**: Deferred to a separate future task.
- **Conscious Trade-off**: Skipped due to time, complexity, performance, or YAGNI (You Aren't Gonna Need It).

This ensures a decentralized, self-documenting codebase where future agents or developers can read the feature history using `git log` rather than consuming tokens reading large directories of markdown logs.
