# Example: Code Patching from a Compiler Error

## Scenario

You have a compilation error such as:

- `Unexpected identifier at line 171`
- or a type error
- or a missing symbol error

Goal: produce a minimal patch that removes the error and preserves behaviour.

## Inputs

- Error message (and stack trace if present)
- Target language and build tool (e.g., Java + Maven)
- Code context:
  - prefer a **focused window** around the error location (e.g., ±30–80 lines)
  - plus any referenced declarations if outside the window

## Loop Template

### Step 1 — Interpret (no code)
Ask:
- “Explain what this error typically means and what kinds of causes it implies.”

Output:
- plain-language meaning
- likely causes
- what evidence would distinguish causes

### Step 2 — Localise and Diagnose (focused code only)
Ask:
- “Given the error and this code region, identify the most likely cause in this specific context.”

Output:
- the precise construct likely triggering the error
- why it is invalid in the given language/syntax

### Step 3 — Propose (prose only)
Ask:
- “Propose the minimal conceptual change to resolve the cause above. Do not write code yet.”

Output:
- a small change described as intent

### Step 4 — Constrain
Add explicit constraints, for example:
- “Do not reformat unrelated code.”
- “Do not rename symbols.”
- “Change only within this method unless strictly necessary.”
- “Prefer the smallest valid diff.”

### Step 5 — Generate Patch (first diff)
Ask:
- “Produce a unified diff implementing exactly the proposal under the constraints.”

Output:
- a minimal patch

### Step 6 — Critique (machine + model)
Run deterministic checks:
- does the patch apply?
- does it compile?
- did the error disappear?
- lines changed / hunks count / files touched

Optionally ask the LLM:
- “Critique this diff against the constraints. Identify any non-essential changes.”

### Step 7 — Refine
Ask:
- “Revise the diff to address the critique and reduce scope.”

Repeat until acceptance criteria are met.

## Acceptance Criteria

- Patch applies cleanly
- Compilation succeeds (or at least the target error is removed)
- Diff is minimal and targeted
- No unrelated changes

## Common Failure Modes

- Incorrect anchoring (context doesn’t match file)
- Overreach (large refactors unrelated to the error)
- Underreach (patch doesn’t address root cause)
- Oscillation (alternates between two imperfect fixes)

In all cases: force smaller steps, tighter constraints, and stronger checks.
