# The Guided Convergence Loop

## Definition

The **Guided Convergence Loop (GCL)** is a structured interaction pattern for working with LLMs in which intermediate artifacts are produced, evaluated, and iteratively refined under explicit constraints until acceptance criteria are met.

The loop externalises reasoning steps that are often implicit in “reasoning models”, making the process:

- more **inspectable** (you can see intermediate decisions),
- more **controllable** (you can add constraints and guardrails),
- more **robust** (smaller steps reduce error compounding),
- more **cost-effective** (cheaper models can perform well under scaffolding).

## Core Phases

### 1) Interpret
Goal: produce a clear explanation of the input.

Typical inputs:
- compiler error messages
- failing tests
- user requirements
- ambiguous prompts
- logs or stack traces

Outputs:
- plain-language meaning
- likely classes of causes
- what evidence would disambiguate causes

### 2) Propose
Goal: generate an initial candidate solution.

Key guideline:
- Prefer **prose proposals** before patches/code for stability.
- Keep scope local: identify the smallest viable change.

Outputs:
- an approach
- a hypothesised fix
- a shortlist of candidate changes

### 3) Constrain
Goal: enforce constraints that the LLM will not reliably infer.

Examples:
- “minimal diff”
- “no formatting-only changes”
- “change only within file X”
- “do not rename symbols”
- “must pass tests A and B”
- output format rules (diff, JSON, bullet list, etc.)

Outputs:
- explicit constraints, ideally machine-checkable

### 4) Critique
Goal: evaluate the proposal against constraints and reality.

Critique can combine:
- human review
- deterministic checks (lint, compile, patch-apply)
- quantitative measures (lines changed, hunks touched)
- LLM self-critique (as a reviewer, not an author)

Outputs:
- specific deficiencies
- ranked issues
- actionable revision instructions

### 5) Refine
Goal: produce a revised artifact that addresses critique with minimal new change.

Key guideline:
- Treat refinement as **editing**, not re-generation.
- Prefer stable intermediate representations (e.g., “proposal text” → “diff”).

Outputs:
- a smaller, more targeted patch/plan
- improved adherence to constraints

### 6) Converge
Goal: repeat until acceptance criteria are met—or stop with a clear failure reason.

Acceptance criteria examples:
- patch applies cleanly
- compilation succeeds
- tests pass
- diff is minimal and local
- the original error is eliminated

Failure conditions should also be explicit:
- no progress after N iterations
- repeated oscillation
- constraints cannot be satisfied simultaneously

## Practical Notes

- **Confidence is a system property**: add observability (checks, metrics) rather than “trusting the model”.
- **Reduce entropy early**: explanation and localisation before editing.
- **Prefer small reversible steps**: each step should be easy to validate and roll back.
