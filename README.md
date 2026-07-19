# Lightweight Engineering (`le`)

A **highly customizable, general-purpose AI-first framework** specifically designed for **Antigravity 2.0**.

This plugin eliminates all the heavy multi-agent loops and token-draining workflows of **Compound Engineering** and **Superpowers**. It replaces markdown specs, plans, and logs with a decentralized, zero-dependency git-commit workflow, a strict bug-to-autotest policy, and targeted, token-efficient research.

---

## The Three Core Rules

This skeleton plugin bootstraps your AI agent with exactly three rules:

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

### 3. Strict Target-Driven Investigation & Research
To prevent token waste, off-topic web search loops, and unnecessary file scanning:
- **No Blind Scanning**: The agent will not scan directories recursively, search blindly, or read files outside the direct scope of the task.
- **Thought-First Investigation Planning**: Before using any investigation tool (`view_file`, `list_dir`, `grep_search`, `search_web`), the agent must write down a quick target plan in its thoughts explaining *what specific information/file it needs to find and why*.
- **Strict Web Search Constraints**: Web searches are restricted strictly to technical docs, syntax references, or compiler error messages. General-knowledge or unrelated searches are banned.
- **Strict Workspace Boundaries**: The agent will never read, search, or list files in paths outside the active project root (e.g. user home directories, system folders, App Data).

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
