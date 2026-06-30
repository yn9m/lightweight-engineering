---
name: le:code-review
description: Runs a thorough code review. It extracts changes between two commits (or active changes) and dispatches two concurrent subagents (Code Reviewer and Security Auditor) before synthesizing a final unified report.
argument-hint: "[base commit SHA] [head commit SHA]"
---

# Code Review Orchestrator

Use this skill to perform a thorough, multi-agent review of code changes. This is the only skill in this toolkit permitted to spawn subagents.

## Execution Flow

### Step 1: Resolve Git Range
Determine the range of commits to review.
- If SHAs are provided in the arguments, use them: `BASE_SHA` and `HEAD_SHA`.
- If no SHAs are provided, use git commands to identify:
  - Active uncommitted changes (diff against HEAD), OR
  - The last commit (`git rev-parse HEAD~1` to `git rev-parse HEAD`), OR
  - Compare the current branch to `origin/main` or `main`.
- Generate the diff stats and content:
  ```bash
  git diff --stat BASE_SHA..HEAD_SHA
  git diff BASE_SHA..HEAD_SHA
  ```

### Step 2: Spawn Concurrent Subagents
Launch **two subagents concurrently** using the platform's parallel subagent execution tool (`invoke_subagent`):

1. **Subagent 1: Senior Code Reviewer**
   - **Role**: Code Quality Reviewer
   - **Workspace**: inherit
   - **Prompt**:
     ```text
     Review these code changes for functionality, logic, architecture, and testing.
     Use the instructions in the template file: `skills/code-review/code-reviewer.md`.
     
     Git Diff:
     [Insert Diff here]
     ```

2. **Subagent 2: Security Auditor**
   - **Role**: Security Auditor
   - **Workspace**: inherit
   - **Prompt**:
     ```text
     Audit these code changes strictly for security vulnerabilities, secrets leaks, and compliance issues.
     Use the instructions in the template file: `skills/code-review/security-auditor.md`.
     
     Git Diff:
     [Insert Diff here]
     ```

### Step 3: Synthesize Findings
Once both subagents complete their audits and report back:
1. Read their findings.
2. Combine and format the results into a single **Unified Audit Report**.
3. Group findings by severity (Critical, Important, Minor) and provide a final verdict on whether the code is ready to merge.

## Unified Audit Report Format

### 🛡️ Unified Audit Report

### 1. Strengths
- [Consolidated strengths from both reports]

### 2. Issues

#### 🚨 Critical (Must Fix)
- [Bugs, data loss risks, credentials leaks, SQL injections, authorization flaws, broken behavior]

#### ⚠️ Important (Should Fix)
- [Architectural problems, test coverage gaps, weak input validations, minor security risks]

#### 📝 Minor (Nice to Have)
- [Style issues, minor optimizations, docstrings, formatting]

### 3. Recommendations
- [Consolidated tips for quality and security]

### 4. Assessment
- **Ready to Merge**: [Yes | No | With fixes]
- **Reasoning**: [1-2 sentences summarizing the assessment]
