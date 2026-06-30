---
name: le:log
description: Run this at the end of each task or feature implementation to create/update the feature's specific log file under docs/features/.
argument-hint: "[feature name]"
---

# Feature Development Logging

Use this skill at the end of every feature development session or task to write or update a clean, per-feature log file.

This skill runs strictly in the main chat context.

## Action Steps

### Step 1: Create or Update Log File
Write the log file to:
`docs/features/<feature-name>-log.md`

### Step 2: Fill in the Mandated Structure

Each log file **must** use this structure:

```markdown
# Feature Log: [Feature Name]
Date: YYYY-MM-DD
Branch: [git branch name]

## 1. What Was Done
- **Core Changes**: [Summary of the main implementation.]
- **Files Modified/Created**:
  - `[relative path]` ([brief description of edits])
- **Decisions & Architecture**: [Key technical decisions or assumptions made.]

## 2. What Was NOT Done & Why (MANDATORY)
List everything that was omitted, deferred, or skipped. Group each item by one of these three categories:

### 🚫 By Design (Core Architecture Decisions)
- [Detail what was avoided by design and the architectural reason why (e.g. avoided server-side state to keep it stateless).]

### ⏳ Out of Scope (Deferred to Future Tasks)
- [Detail what belongs in a separate future task and why it was deferred (e.g., pagination postponed to keep the initial PR simple).]

### ⚖️ Conscious Trade-offs (Decisions based on constraints/trade-offs)
- [Detail what was skipped due to trade-offs (e.g., using simpler in-memory array search instead of building a full index because of YAGNI).]

## 3. Next Steps
- [1-3 action items for the next developer or agent session to build on top of this work.]
```

Provide the user with a clickable link to the created/updated log file.
