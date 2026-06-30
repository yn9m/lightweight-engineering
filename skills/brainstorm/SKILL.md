---
name: le:brainstorm
description: Run this before starting work on any feature or major modification. It guides collaborative requirements elicitation, performs logical pressure testing, outputs a requirements doc, and automatically logs.
argument-hint: "[feature name or idea]"
---

# Brainstorm Feature Requirements

Use this skill to turn vague ideas, feature requests, or improvements into a solid, clear requirements document through a collaborative dialogue.

This skill runs strictly in the main chat context.

## Strict Rule: Product Logic ONLY
- **Never ask technical or implementation questions** during the brainstorming stage.
- Do NOT ask about database tables, schemas, file paths, directories, libraries, frameworks, programming languages, or API designs.
- All technical and implementation details are strictly deferred to the `/le:plan` stage.
- Focus exclusively on: *What is the goal? Who is the user? What is the user experience? What are the edge cases of the business logic?*

---

## Action Steps

### Step 1: Functional Elicitation (One Question at a Time)
- Ask clarifying questions about user behavior, input requirements, expected output, and scope boundaries.
- **Rule**: Ask exactly **one question per turn** to keep the dialogue focused.
- Prefer multiple-choice options to scaffold the user's responses.

### Step 2: Adversarial Pressure Testing (Try to Break the Idea)
Before wrapping up and writing the requirements document, you **must** pause and critically re-evaluate the gathered context:
1. **Adversarial Assessment**: Actively search for gaps, contradictions, unstated assumptions, or logical failures in the proposed flow.
2. **Break the logic**: Think about what happens in extreme user scenarios (e.g., concurrent actions, unexpected cancellations, logic loops, permission conflicts).
3. **Ask the Pressure Test Question**: Formulate and ask at least one deep, critical question based on this re-evaluation to challenge and refine the feature's design.

### Step 3: Write Requirements Document
Once approved, write the requirements document to:
`docs/brainstorms/YYYY-MM-DD-<feature-name>-requirements.md`

#### Requirements Document Template:
```markdown
# Requirements: [Feature Name]
Date: YYYY-MM-DD

## 1. Goal & Context
[Explain the problem being solved and user value.]

## 2. User-Facing Behavior & Flow
[Step-by-step description of the user experience and logical flow.]

## 3. Scope Boundaries & Constraints
- **In Scope**: [What is built.]
- **Out of Scope (Deferred)**: [What is deliberately omitted or postponed.]

## 4. Edge Cases & Logical Exceptions
- [Handling of user errors, logical loops, empty inputs, or cancellations.]

## 5. Success Criteria
- [How we verify the feature behaves correctly from a business perspective.]
```

### Step 4: Automate Logging (MANDATORY)
Immediately after saving the requirements document, **automatically execute the logging logic (`le:log`)** to create/update `docs/features/<feature-name>-log.md`:
- Record that the brainstorm was completed and the requirements file was created.
- Document any decisions made, what was included, and explicitly log what was marked **Out of Scope** or deferred as a **Conscious Trade-off**.

Provide the user with clickable links to both the requirements document and the updated feature log file.

## Next Steps (Handoff)
- Explain to the user that the requirements are finalized, and the next step is **mandatory planning** using `/le:plan [feature-name]`.
