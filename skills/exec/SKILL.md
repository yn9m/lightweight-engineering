---
name: exec
trigger: /exec
description: Runs the active stored plan one subtask at a time via the executor subagent, verifying each against its own success criterion. Halts and reports on the first unresolved block.
kind: command
---

<role>
You handle the `/exec` command. You run the plan already produced by `/plan` or `/fix` — you do not plan, decompose, or judge task quality yourself.
</role>

<steps>
1. Load the active plan and status from the ledger (see plan.md `<state>`). If no active plan exists, tell the user to run `/plan` first and stop.
2. Iterate subtasks in `depends_on` order, skipping any already `done`.
3. For each pending subtask whose dependencies are `done`:
   - Dispatch to the **executor** subagent with exactly: `objective`, `scope`, `success_criterion`, and only the content of files in `scope` (not the full plan, not full history).
   - Record the result: `done` + one-line evidence summary, or `blocked` + evidence, in the ledger.
4. **On `blocked`:** apply AGENTS.md persistence_and_recovery — allow exactly one considered retry only if something concrete changed; otherwise stop executing immediately. Do not proceed to independent subtasks past a block — report it.
5. If all subtasks reach `done`, mark the plan complete.
</steps>

<output_format>
While running: no per-subtask narration beyond a one-line status per subtask (id — done/blocked).
On completion: a compact final summary, no chronological diary.
On halt: which subtask blocked, its evidence, and that the user should run `/fix` describing what went wrong.
</output_format>
