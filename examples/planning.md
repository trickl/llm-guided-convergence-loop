# Example: Planning a Multi-Step Task

## Scenario

You want an LLM to produce a plan for a multi-step engineering task (e.g., add a feature, migrate a subsystem, refactor safely).

Goal: produce a plan that is executable, scoped, and robust to missing information.

## Inputs

- Objective (what “done” means)
- Constraints (time, risk tolerance, allowed changes)
- Environment (repo layout, language, build system)
- Known unknowns

## Loop Template

### Step 1 — Interpret
Ask:
- “Restate the objective and constraints. List assumptions and unknowns.”

### Step 2 — Propose a Draft Plan
Ask:
- “Produce a step-by-step plan with checkpoints and expected artifacts.”

### Step 3 — Constrain
Add constraints such as:
- limit scope per step
- require validation checkpoints
- require rollback strategy
- forbid speculative changes without evidence

### Step 4 — Critique the Plan
Ask:
- “Review this plan for risk, missing dependencies, unclear steps, and verification gaps.”

### Step 5 — Refine
Ask:
- “Rewrite the plan to address critique while keeping it minimal and actionable.”

### Step 6 — Converge
Repeat until:
- steps are unambiguous
- each step has a validation mechanism
- failure handling is explicit

## Acceptance Criteria

- Each step has: inputs, action, output, validation
- Clear ordering and dependencies
- Explicit checks (tests, builds, metrics)
- Minimal assumptions; unknowns called out early
