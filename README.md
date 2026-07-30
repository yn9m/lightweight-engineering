# Lightweight Engineering (`le`)

A **highly customizable, token-efficient AI-first framework** specifically designed for **Antigravity 2.0**.

This plugin eliminates the heavy, token-draining workflows of older AI frameworks (like generating endless markdown specs, plans, and logs). Instead, it enforces a lean, decentralized approach using Git commit history as persistent memory, strict fact-first debugging, and specialized subagents. 

It acts as an overlay on top of the global `AGENTS.md` ruleset, providing specialized behaviors without duplicating standard constraints.

---

## Core Features

This plugin bootstraps your AI agent with the following strict workflow constraints:

### 1. Bug-to-Autotest Guarantee
Whenever the agent debugs or fixes a bug, it is strictly prohibited from guessing the cause. It must gather facts first. Once the root cause is verified and fixed, it **must** write an automated test (unit or integration) that reproduces the bug (fails before the fix, passes after). 

### 2. Decentralized Git Persistent Memory
Writing and reading separate `.md` log files or requirements specs consumes a massive amount of context tokens. 
- **No Markdown Logs**: The agent is forbidden from creating `.md` log files.
- **Git Commits as Memory**: Progress is documented directly inside the **Git commit message** using a specific Conventional Commits format that tracks what was done, and explicitly what was **NOT done & Why** (By Design, Out of Scope, Conscious Trade-off).
- Future agents are instructed to use `git log` to retrieve past context and architectural decisions.

### 3. Specialized Subagent Delegation
The orchestrator must not pollute its own context with endless search loops or debugging trials.
- **`researcher` Subagent**: Mandatory for gathering context from local repositories, reading official documentation, or looking up external web references.
- **`debugger` Subagent**: Mandatory for localizing the root cause of reproducible runtime failures and behavioral defects. It diagnoses the issue and returns an evidence-backed repair plan without blindly editing files.

*(Note: Standard investigation rules, process monitoring, and routine task delegation principles are inherited from the global `AGENTS.md` file included in this repository).*

---

## Plugin Structure

- `skills/using-le/SKILL.md` - The primary bootstrap skill that establishes the core workflow (Commits as Memory, Autotests, Subagent triggers).
- `agents/researcher.md` - Subagent instruction for context gathering and documentation research.
- `agents/debugger.md` - Subagent instruction for evidence-backed root cause localization.
- `AGENTS.md` - Global behavioral rules (anti-looping, strict workspace boundaries, syntax pre-checking) applied across the workspace.

---

## Installation

Clone this repository into your AI client's plugin directory:

### For Antigravity 2.0:
1. Place the `lightweight-engineering` folder into:
   - **Windows**: `C:\Users\<Your-Username>\.gemini\config\plugins\`
   - **macOS/Linux**: `~/.gemini/config/plugins/`
2. Start a new session. The `le:using-le` skill will bootstrap automatically.

---

## License

This project is licensed under the [MIT License](LICENSE).
