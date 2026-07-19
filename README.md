# Lightweight Engineering (`le`)

A **highly customizable, general-purpose AI-first framework** specifically designed for **Antigravity 2.0**.

This plugin eliminates all the heavy multi-agent loops and token-draining workflows of **Compound Engineering** and **Superpowers**. It replaces markdown specs, plans, and logs with a decentralized, zero-dependency git-commit workflow, a strict bug-to-autotest policy, fact-first debugging, targeted research, and smart subagent delegation.

---

## The Five Core Rules

This skeleton framework bootstraps your AI agent with exactly five rules:

### 1. Bug-to-Autotest Guarantee & Fact-First Debugging
- **Fact-First Debugging**: The agent is strictly prohibited from guessing the cause of bugs or proposing changes without evidence. It must gather facts first (check errors, verify code lines, analyze logs). If context is lacking, it must ask clarifying questions or propose diagnostic commands rather than making assumptions.
- **Regression Testing**: Whenever the agent debugs or fixes a bug in the codebase, it **must** write an automated test (unit/integration) that reproduces the bug (fails before the fix, passes after) before completing the task. This ensures the bug never recurs and locks in debug findings as code.

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
- **Ask for Paths (No Recursive Crawling)**: If the agent needs to access a specific file and does not know its path, or if the project has a large directory structure, it is strictly forbidden from running recursive file searches or listings. It must simply ask the user to provide the path in chat.
- **Thought-First Investigation Planning**: Before using any investigation tool (`view_file`, `list_dir`, `grep_search`, `search_web`), the agent must write down a quick target plan in its thoughts explaining *what specific information/file it needs to find and why*.
- **Strict Web Search Constraints**: Web searches are restricted strictly to technical docs, syntax references, or compiler error messages. General-knowledge or unrelated searches are banned.
- **Strict Workspace Boundaries**: The agent will never read, search, or list files in paths outside the active project root (e.g. user home directories, system folders, App Data).

### 4. Active Process Monitoring & Anti-Dangling Rule
To prevent hanging processes and undetected failures:
- **Pre-check Syntax**: Always verify syntax correctness of your scripts before executing them.
- **Monitor Async Tasks**: When running background commands, verify status/logs using `manage_task` immediately after launching to detect early crashes or syntax errors.
- **Handle Early Failures**: If a script exits immediately with an error, capture output and address it immediately rather than waiting blindly.
- **Kill Unresponsive Tasks**: If a task hangs or goes into an infinite loop, terminate it immediately using `manage_task` with action `kill`.

### 5. Smart Subagent Delegation & Model Scaling
To optimize token usage and automate routine mechanical work:
- **Do Not Direct the User to Do Dirty Work**: The agent must never instruct the user to manually perform routine mechanical tasks (like copying/moving files, renaming directories, editing single lines, or running simple installs/commands). It must spawn a subagent to handle this automatically.
- **Reasoning Complexity Assessment**: Before spawning a subagent, the agent must evaluate the task's complexity by depth (not size or quantity):
  - **Low-Reasoning Tasks (Mechanical/Routine)**: Editing simple syntax, renaming/moving files, performing basic checks. Delegate to a subagent using a cheap, low-reasoning model: `flash_lite` or `flash` to save tokens.
  - **High-Reasoning Tasks (Deep/Complex)**: Complex logic changes, multi-file refactoring, writing complex tests, or solving deep runtime bugs. Delegate using `inherit` or `pro` models.

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
