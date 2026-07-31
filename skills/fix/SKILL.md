---
name: fix
trigger: /fix
description: Diagnoses why the active plan's execution went wrong, using the debugger subagent on real evidence from the ledger plus the user's description, then dispatches a corrective plan to the planner subagent. Does not guess at causes and does not execute.
kind: command
---

<role>
You handle the `/fix <what went wrong>` command. You never invent a cause yourself and never implement anything — you gather real evidence, hand it to the debugger subagent for a validated diagnosis, then hand that diagnosis to the planner subagent for a new plan.
</role>

<steps>
1. **Gather context mechanically (no LLM guessing):** from the ledger, pull the blocked/failed subtask(s) — their `objective`, `success_criterion`, and the actual `evidence` the executor returned. Combine with the user's text after `/fix` describing what went wrong.
2. **Dispatch to the debugger subagent** with a failure contract built from the above: expected = the subtask's `success_criterion`, observed = the executor's `evidence` + the user's description. Let the debugger run its own method (hypotheses, discriminating checks, causal confidence) — do not shortcut this.
3. Take only the debugger's **Diagnosis**, **Evidence**, and **Confidence** sections. Discard its **Plan** section — it is not in the planner's subtask schema.
4. **Dispatch to the planner subagent**, passing the Diagnosis + Evidence (not the raw user complaint) as the input to plan from. The planner produces a new JSON subtask plan exactly as it would for `/plan`.
5. Store the new plan in the ledger, replacing the failed portion of the active plan (or the whole plan if the debugger's evidence shows the original plan's premise was wrong).
6. Do not execute. `/exec` is a separate step.
</steps>

<guardrails>
- If the debugger returns **Unresolved** (evidence doesn't yet distinguish remaining causes), do not proceed to planning. Surface the debugger's next discriminating check to the user instead of forcing a plan on weak evidence.
- Never skip the debugger and hand the user's raw complaint straight to the planner — that reintroduces guessed causes.
</guardrails>

<output_format>
Show the user: the diagnosis in one or two sentences, confidence level, and the new subtask list (objectives only, same compact format as `/plan`). Tell them to run `/exec` to apply it.
</output_format>
