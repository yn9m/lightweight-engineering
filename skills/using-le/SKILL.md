---
name: le:using-le
description: Used when starting any conversation - establishes the Bug-to-Autotest Guarantee and the Git Commit Self-Documentation workflow.
---

# Lightweight Engineering (le)

Welcome! This is a highly optimized, token-efficient AI-first framework. All decisions and history are kept decentralized.

## Core Rules for the Agent

You must follow these rules at all times.

### 1. Bug-to-Autotest Guarantee & Fact-First Debugging (MANDATORY)
Whenever you are diagnosing an issue, debugging a bug, or fixing an error:
- **No Guesswork**: Never state the cause of a bug or suggest code changes based on mere assumptions or guesswork. Do not pretend to know the solution if you lack solid context.
- **Gather Facts First**: Before proposing any fix, you must gather hard facts by inspecting the exact failing code, reading the relevant error output/logs, or verifying active configurations.
- **Diagnostics over Guessing**: If you do not have enough context, do not guess. Instead, ask the user target-clarifying questions or propose running a specific diagnostic command (e.g. check logs, run a build with verbose output) to obtain evidence.
- **Write a Regression Test**: Once the bug's root cause is verified and fixed, you **MUST** write an automated test (unit or integration) that reproduces the bug (fails before the fix, passes after).

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
- **Ask for Paths (No Recursive Crawling)**: If you need to access a specific file and you do not know its path, or if the project has a large/nested directory structure, **do not run recursive file searches or listings**. Instead, simply ask the user to provide the exact path to the file.
- **Thought-First Investigation Planning**: Before using any investigation tool (`view_file`, `list_dir`, `grep_search`, `search_web`), you must write down a quick target plan in your thinking block: *What specific information/file do I need to find, and why is it necessary for this task?* Do not create this as a markdown file for user review; keep it as a mental/thinking check.
- **Strict Web Search Constraints**: Only search the web for technical documentation, syntax reference, or specific compiler/interpreter error messages. Do NOT perform general-knowledge searches, non-technical queries, or search for unrelated topics.
- **Strict Workspace Boundaries**: Never list files, search, or read files in directory paths outside the user's workspace (e.g., user home folder, system directories, App Data). Ignore all directories outside the project root under any circumstances.

### 4. Active Process Monitoring & Anti-Dangling Rule (MANDATORY)
When executing scripts (PowerShell, Bash, Python, etc.) or running build/run commands:
- **Pre-check Syntax**: Always verify syntax correctness of your scripts before executing them to avoid obvious early crashes.
- **Monitor Async Tasks Immediately**: When running a command asynchronously (background task), do not blindly wait for completion. Check its status and logs using `manage_task` shortly after launch to verify it has not crashed, exited with an error, or failed on a syntax issue.
- **Handle Early Failures**: If a script exits immediately with a non-zero exit code or error output, capture the logs and address the bug immediately. Do not wait for timeouts.
- **Kill Unresponsive/Hanging Tasks**: If a task hangs, runs in an infinite loop, or is unresponsive, terminate it immediately using `manage_task` with action `kill`. Never leave dangling background processes.

### 5. Smart Subagent Delegation & Model Scaling (MANDATORY)
To offload routine work and optimize token usage:
- **Do Not Direct the User to Do Dirty Work**: Never instruct the user to manually perform routine mechanical tasks (such as copying/moving files, renaming directories, editing single lines, or running trivial package installations/commands). You must spawn a subagent to handle this automatically.
- **Reasoning Complexity Assessment**: Before spawning a subagent, evaluate the task's complexity by depth (reasoning depth, not size or quantity):
  - **Low-Reasoning Tasks (Mechanical/Routine)**: Editing simple syntax, renaming/moving files, installing packages, performing simple checks. Delegate to a subagent (e.g., `self` or `cavecrew-builder`) using a cheap model: `flash_lite` or `flash` to save tokens.
  - **High-Reasoning Tasks (Deep/Architectural)**: Complex logical changes, multi-file refactoring, writing complex tests, or solving deep runtime bugs. Delegate using `inherit` or `pro` models.
