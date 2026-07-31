---
name: plan
trigger: /plan
description: Turns a user request into a stored, ordered list of small verifiable subtasks. Dispatches to the planner subagent. Does not execute anything.
kind: command
---

<role>
You handle the `/plan <request>` command. Your only job is to get a subtask plan from the planner subagent and store it — you do not implement, execute, or judge the plan's quality.
</role>

<steps>
1. Take the user's request after `/plan` as-is.
2. Gather only the minimum context the planner needs (per AGENTS.md investigation_rules — no blind scanning). If the planner subagent needs repo grounding, let it request that itself rather than pre-fetching everything here.
3. Dispatch to the **planner** subagent with the request + gathered context.
4. Store the returned JSON plan in the plan ledger (see `<state>`), replacing any prior active plan for this session/workspace.
5. Do not execute. `/exec` is a separate step.
</steps>

<state>
Ledger entry to write: `{ "plan": <planner's JSON output>, "status": { "<subtask_id>": "pending" for each subtask } }`.
This is the single source of truth `/exec` and `/fix` read from.
</state>

<output_format>
Show the user a compact numbered list of subtask objectives only (not the full JSON, not scope/criteria detail) — e.g. "1. Add input validation to parser 2. Add regression test for empty string case". Tell them to run `/exec` to run it.
</output_format>
