# Lightweight Engineering (`le`)

A **highly customizable, general-purpose AI-first framework** specifically designed for **Antigravity 2.0**.

This plugin eliminates all the heavy multi-agent loops and token-draining workflows of **Compound Engineering** and **Superpowers**. It replaces markdown specs, plans, and logs with a decentralized, zero-dependency git-commit workflow and a strict bug-to-autotest policy.

---

## The Two Core Rules

This skeleton plugin bootstraps your AI agent with exactly two rules:

### 1. Bug-to-Autotest Guarantee
Whenever the agent debugs or fixes a bug in the codebase, it **must** write an automated test (unit/integration) that reproduces the bug (fails before the fix, passes after) before completing the task. This ensures the bug never recurs and locks in debug findings as code.

### 2. Decentralized Commit Self-Documentation
Instead of creating and reading separate `.md` log files or requirements specs (which is highly token-expensive), the agent documents its progress directly inside the **Git commit message**.

Every commit prepared by the agent **must** use this template:

```text
[feat/fix/chore]: <short description in Conventional Commits format>

### What was done:
- [relative file path] - [brief description of changes]

### What was NOT done & Why (MANDATORY):
- <item omitted/deferred> [By Design: explanation]
- <item omitted/deferred> [Out of Scope: explanation]
- <item omitted/deferred> [Conscious Trade-off: explanation]
```

This creates a self-documenting git history that any future agent or developer can search using `git log` rather than consuming tokens reading large directories of markdown logs.

---

## Installation

Clone this repository into your AI client's plugin directory:

### For Antigravity 2.0 / Claude Code:
1. Place the `lightweight-engineering` folder into:
   - **Windows**: `C:\Users\<Your-Username>\.gemini\config\plugins\` or `C:\Users\<Your-Username>\.claude\plugins\`
   - **macOS/Linux**: `~/.gemini/config/plugins/` or `~/.claude/plugins/`
2. Start a new session. The `le:using-le` skill will bootstrap automatically.

---

## License

This project is licensed under the [MIT License](LICENSE).
