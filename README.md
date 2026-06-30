# Lightweight Engineering (`le`)

A **highly customizable, general-purpose AI-first framework** specifically designed for **Antigravity 2.0**.

> [!IMPORTANT]
> **This is a skeleton framework.** It is not a rigid out-of-the-box solution, but a highly adaptable boilerplate. Every developer is expected to customize the templates, files, and rules in the `skills/` directory to suit their own tech stack, languages, architecture, linting configurations, and quality gates.

---

## Philosophy & Origin

This framework was created out of frustration with existing tools like **Compound Engineering** and **Superpowers**. While those toolkits introduce excellent software engineering patterns, they often lead to excessive token consumption by spawning heavy, recursive multi-agent execution loops for simple actions.

**Lightweight Engineering** takes the best concepts from both worlds:
- Collaborative product brainstorming
- Structured, dependency-aware step-by-step planning
- Feature-level action logging
- Isolated, deep code auditing

Our goal is to **preserve the AI-first development philosophy** while **drastically reducing token waste** on redundant or low-value agent processes. All workflows (except code review) run directly inside the main chat context.

---

## Key Features

1. **Strict Separation of Concerns**:
   - **`/le:brainstorm` (Product Logic)**: Collects requirements and defines scope. Forbidden from asking technical details (files, DB, code stack).
   - **`/le:plan` (Technical Design)**: Focuses strictly on implementation steps, code locations, DB schema, and endpoints. Requires a prior brainstorm document.
2. **Automated Per-Feature Logging (`/le:log`)**:
   - Automatically maintains concise history files (`docs/features/<feature-name>-log.md`) keeping track of what was done, what was **not** done, and the **reasoning** behind decisions (*By Design*, *Out of Scope*, *Conscious Trade-offs*).
3. **Mandatory Regression Testing**:
   - Any bug found and fixed during debugging must be covered by a regression test (fails before the fix, passes after) to lock in context and save tokens in future runs.
4. **Dual-Agent Code Review (`/le:code-review`)**:
   - Spawns two concurrent subagents (Code Quality Reviewer & Security Auditor) to audit the diff and output a single, unified report.

---

## Directory Structure

When initialized with `/le:setup`, the plugin sets up the following structure in your project:

```
docs/
├── brainstorms/    # Requirements specs (docs/brainstorms/YYYY-MM-DD-<feature>-requirements.md)
├── plans/          # Implementation plans (docs/plans/YYYY-MM-DD-<feature>-plan.md)
├── features/       # Localized feature logs (docs/features/<feature>-log.md)
├── solutions/      # Architectural patterns and reusable solutions
├── Testing.md      # Testing strategy (80-90% Unit test coverage focus)
├── Security.md     # Secrets, validation, and SAST criteria
└── DefinitionOfDone.md  # Completion checklist (Conventional Commits, Regression tests)
```

---

## Available Commands

- **`/le:setup`**: Initializes folder structure and writes project quality standard markdown files.
- **`/le:brainstorm [feature]`**: Explores requirements and performs an adversarial pressure test. Writes requirements to `docs/brainstorms/`.
- **`/le:plan [feature]`**: Gathers technical stack, schema, and API structure. Writes plan to `docs/plans/`.
- **`/le:log [feature]`**: Updates log files and tracks deferred tasks / trade-offs.
- **`/le:code-review [base commit] [head commit]`**: Runs parallel code quality and security reviews.

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
