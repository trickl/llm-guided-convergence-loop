# LLM-Guided Convergence Loop

This repository explores a structured approach to using Large Language Models (LLMs) for complex problem-solving tasks—particularly code patching—by decomposing the task into a sequence of focused stages with feedback between each step.

The central idea is that LLMs perform significantly better when they are guided through **an explicit loop** rather than asked to diagnose, reason, and act in a single prompt.

---

## Motivation

LLMs are powerful, but they are not reliable when used monolithically.

In particular, they struggle when asked to:
- interpret an error
- infer root causes
- propose fixes
- and emit patches

all at once.

Once an LLM commits to an early interpretation, it tends to defend and elaborate that interpretation—even when it is incorrect.

This repository explores how **decomposition and iteration** can be used to extract the maximum benefit from LLMs while mitigating those weaknesses.

---

## The Core Idea: The Loop

Instead of a single prompt, we structure problem-solving as a loop of smaller, narrowly scoped stages.

At a high level, the loop looks like this:

1. **Interpret**  
   Interpret external feedback (e.g. compiler errors, test failures) without proposing fixes.

2. **Diagnose**  
   Form a hypothesis about the underlying cause of the failure.

3. **Propose**  
   Describe the intent of a change that would address the diagnosis.

4. **Patch**  
   Emit a concrete patch implementing that intent.

5. **Validate**  
   Apply the patch and observe the new feedback.

6. **Refine or Repeat**  
   Use the new information to refine the diagnosis or restart the loop.

By separating these concerns, each LLM invocation has a clear objective and a narrower search space.

---

## Why Decomposition Works

This staged loop improves outcomes because it aligns with LLM strengths:

- focused reasoning over small scopes
- local consistency within a single step
- responsiveness to explicit feedback

It also makes failures easier to inspect, since each step has a clearly defined responsibility.

---

## Refinement Alone Is Not Enough

In practice, decomposition and iteration solve many problems—but not all.

A key limitation emerges once the loop runs for multiple iterations:

> **LLMs tend to strongly commit to early diagnoses.**

When this happens, the loop continues to run, but each iteration merely refines or defends the same incorrect hypothesis. Patches fail, errors remain unchanged, yet the diagnosis persists.

This failure mode is referred to here as **hypothesis lock-in**.

---

## Avoiding Hypothesis Lock-In

To preserve the benefits of decomposition while avoiding stagnation, the loop must treat diagnoses as **explicit, replaceable hypotheses**, rather than as assumptions that silently persist across iterations.

The loop is therefore augmented with the following structural constraints:

- Each diagnosis is treated as a discrete hypothesis
- Each patch corresponds to exactly one hypothesis
- Hypotheses must be falsifiable by observable outcomes
- Repeated failure weakens or rejects hypotheses
- Patches must introduce meaningful structural change
- Stalled iterations force exploration of alternatives

These safeguards operate at the level of **process**, not language or syntax, and therefore scale across domains.

---

## What This Loop Optimizes For

The convergence loop is designed to maximize:

- the usefulness of each LLM call
- the signal extracted from external feedback
- the ability to recover from incorrect assumptions
- the likelihood of eventual convergence on a valid solution

It does not attempt to encode:
- programming language rules
- grammar knowledge
- domain-specific semantics

Those remain external sources of feedback.

---

## Repository Structure

- `examples/`  
  Conceptual guides and patterns demonstrating how to apply the loop.

- `examples/code-patching.md`  
  A focused description of iterative, hypothesis-driven code patching and the safeguards required to avoid lock-in.

---

## Guiding Principle

> The power of this approach lies not in asking LLMs better questions, but in asking them *smaller*, *more disciplined* ones—repeatedly, with feedback.

This repository explores how to do that systematically.
