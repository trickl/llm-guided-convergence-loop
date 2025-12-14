# Example: Error Diagnosis Without Editing Code

## Scenario

You have a failing test, a crash, or a runtime error, but you want a reliable diagnosis before changing anything.

Goal: produce a ranked set of plausible causes with suggested evidence-gathering steps.

## Inputs

- Error message / stack trace / logs
- Runtime environment details (versions, flags, platform)
- Minimal reproducer if available
- Relevant code excerpts (small, targeted)

## Loop Template

### Step 1 — Interpret
Ask:
- “Explain what this error indicates, and list likely categories of root causes.”

### Step 2 — Constrain the Hypothesis Space
Provide constraints:
- what changed recently
- what is known to be working
- which components are in/out of scope

Ask:
- “Given these constraints, narrow to the most plausible causes.”

### Step 3 — Critique via Evidence Planning
Ask:
- “For each top cause, what evidence would confirm or refute it quickly?”
- “Suggest the smallest set of checks to disambiguate.”

### Step 4 — Converge on a Working Theory
As you gather evidence, loop:
- update inputs
- ask the model to revise the ranking
- stop when the diagnosis is sufficiently supported

## Acceptance Criteria

- Clear root-cause hypothesis (or small set)
- Specific evidence that supports it
- Concrete next action (fix, rollback, config change, instrumentation)

## Notes

Diagnosis is often where LLMs shine, provided you:
- keep context small and relevant,
- ask for ranked hypotheses,
- and force explicit “what evidence would change your mind?” thinking.
