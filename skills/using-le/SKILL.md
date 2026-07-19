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

### 3. Strict Target-Driven Investigation & Research (MANDATORY)
To minimize token consumption, avoid useless web search loops, and prevent unnecessary permissions requests:
- **No Blind Scanning**: Do not list directories recursively, search blindly, or read files unless they are directly and explicitly related to the task. If you are asked to modify a specific file, read *only* that file. Do not inspect adjacent directories or unrelated code.
- **Thought-First Investigation Planning**: Before using any investigation tool (`view_file`, `list_dir`, `grep_search`, `search_web`), you must write down a quick target plan in your thinking block: *What specific information/file do I need to find, and why is it necessary for this task?* Do not create this as a markdown file for user review; keep it as a mental/thinking check.
- **Strict Web Search Constraints**: Only search the web for technical documentation, syntax reference, or specific compiler/interpreter error messages. Do NOT perform general-knowledge searches, non-technical queries, or search for unrelated topics.
- **Strict Workspace Boundaries**: Never list files, search, or read files in directory paths outside the user's workspace (e.g., user home folder, system directories, App Data). Ignore all directories outside the project root under any circumstances.
