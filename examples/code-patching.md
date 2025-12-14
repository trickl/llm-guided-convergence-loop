# Guided Code Patching via Iterative Refinement

Large Language Models (LLMs) perform poorly when asked to diagnose, solve, and patch a code issue in a single step. This is not primarily due to a lack of knowledge, but due to premature convergence on a single explanation that is then defended and elaborated upon.

This document describes a language-agnostic refinement loop for code patching and highlights the structural safeguards required to ensure convergence toward correct solutions.

---

## Why Single-Pass Patching Fails

A single-pass approach typically asks the model to:

1. Interpret an error
2. Diagnose a cause
3. Propose a fix
4. Emit a patch

Once a diagnosis is selected, the model tends to preserve it, even when contradictory evidence emerges. Subsequent reasoning is often devoted to justifying or refining the initial hypothesis rather than reassessing it.

This behavior leads to internally consistent but incorrect results.

---

## Refinement Improves Outcomes—But Is Not Sufficient

Decomposing the task into multiple steps (interpretation, diagnosis, patching, validation) improves clarity and allows feedback to be incorporated between iterations.

However, **refinement alone does not guarantee convergence**.

Without explicit mechanisms for rejecting incorrect hypotheses, a refinement loop can repeatedly reinforce the same mistake—producing more detailed explanations without making progress toward a valid solution.

---

## Common Failure Mode: Hypothesis Lock-In

A frequent failure mode in iterative patching systems is *hypothesis lock-in*:

- an early diagnosis is treated as correct
- subsequent steps refine or defend that diagnosis
- failed patches do not weaken or replace the hypothesis
- the loop cycles without producing new information

> Refinement without falsification produces consistency, not correctness.

---

## Refinement Loop Invariants

To reliably converge in a language-agnostic setting, the refinement loop must enforce the following invariants.

### 1. Explicit Hypotheses

Each diagnosis must be represented as a discrete, explicit hypothesis rather than free-form narrative text.

A hypothesis should minimally include:
- a concise claim
- the code region it applies to
- an expected observable effect if corrected

---

### 2. One Hypothesis per Patch

Each patch proposal must correspond to exactly one hypothesis.

Patches that attempt to address multiple ideas at once obscure causality and make validation difficult.

---

### 3. Mandatory Falsifiability

Every hypothesis must be falsifiable.

Before proposing a patch, the loop must identify at least one observable outcome that would contradict the hypothesis (for example: unchanged error output, unchanged location, or failed patch application).

Hypotheses that cannot be falsified are not actionable.

---

### 4. Structural Change Requirement

Each patch must introduce a meaningful **structural change** to the failing region, such as:
- regrouping
- changes in nesting
- scope modification
- ordering changes

Superficial edits that do not alter structure are strong indicators of weak or incorrect hypotheses.

---

### 5. Hypothesis Weakening and Rejection

If multiple patch attempts consistent with the same hypothesis fail to produce new information, that hypothesis must be weakened or rejected.

Refinement must not imply indefinite persistence.

---

## Added Loop Step: Hypothesis Falsification

Before generating a patch, the loop must explicitly answer:

- What observable outcome would contradict this hypothesis?
- Has a prior iteration already contradicted it?
- Would the proposed patch change the structure of the failing construct?

If any of these questions cannot be answered satisfactorily, the hypothesis should be discarded and replaced.

---

## Key Takeaway

A successful guided convergence loop is not defined by how well it refines ideas, but by how effectively it abandons incorrect ones.

Decomposition enables progress, but falsification ensures direction.
