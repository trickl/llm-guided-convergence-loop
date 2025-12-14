# LLM Guided Convergence Loop

A practical methodology for working with large language models (LLMs) using explicit, iterative refinement rather than one-shot prompting — when correctness, minimality, and reliability matter more than convenience.

The core idea is simple: treat LLM outputs (plans, patches, analyses, summaries) as *proposals* that improve through constrained iteration. This makes outcomes more reliable, more inspectable, and easier to debug — especially when using smaller or cheaper models.

This repository documents a simple but powerful idea: LLM outputs should be treated as provisional artifacts that improve through guided iteration, not as final answers generated in a single prompt.

---

## Why This Exists

If you have ever experienced any of the following:

- LLM-generated patches that almost work, but subtly break things
- Large, unfocused diffs when you asked for a small fix
- Plausible explanations that collapse under closer inspection
- Strong results from flagship models, followed by poor results from smaller ones
- Difficulty understanding why a model produced a particular answer

…then this repository is for you.

The core problem is not model quality.  
It is the mental model most people use when interacting with LLMs.

---

## The One-Shot Fallacy

Many failures stem from asking an LLM to do too much at once:

> “Here is the error and the code. Fix it.”

This forces the model to simultaneously:

- interpret the problem
- locate the cause
- decide on a fix
- apply constraints implicitly
- emit a formally correct artifact

Errors compound silently, and debugging becomes guesswork.

---

## What This Pattern Changes

The Guided Convergence Loop replaces one-shot prompting with explicit, inspectable steps.

It externalises reasoning that is often hidden inside advanced “reasoning models” and makes it usable, debuggable, and reliable — even with smaller or cheaper models.

This turns LLMs from brittle answer generators into collaborative components in a controlled process.

---

## What This Helps With

The Guided Convergence Loop is especially useful for tasks where precision matters:

- Fixing compiler or runtime errors with minimal patches
- Generating diffs that must apply cleanly
- Diagnosing failures before changing code
- Planning multi-step engineering work
- Building LLM-driven tools that must be reliable, testable, and cost-efficient

This pattern is less about creativity, and more about engineering discipline applied to LLMs.

---

## The Loop

The Guided Convergence Loop pattern is an explicit sequence of phases:

- **Interpret** — explain what the input means (e.g. an error message, a failing test, a requirement)
- **Propose** — generate a candidate solution or approach, often in prose
- **Constrain** — apply explicit scope, format, and correctness constraints
- **Critique** — evaluate the proposal against constraints and objective signals
- **Refine** — update the artifact to address critique with minimal additional change
- **Converge** — repeat until acceptance criteria are met, or fail fast with a clear diagnosis

Each phase reduces uncertainty and makes the next step safer.

---

## A Discovered Limitation: Hypothesis Lock-In

In practice, applying the loop reveals a second-order failure mode.

Once an LLM forms an initial diagnosis, it may continue to refine and defend that diagnosis even when external feedback contradicts it. The loop continues to run, but progress stalls.

This is referred to as *hypothesis lock-in*.

---

## Refining the Loop

To address this, diagnoses should be treated as explicit, replaceable hypotheses rather than implicit assumptions that persist across iterations.

In practice, this means:

- making diagnoses explicit
- tying each refinement to a single hypothesis
- requiring observable signals that can falsify a hypothesis
- weakening or rejecting hypotheses that repeatedly fail

These refinements preserve the original loop while ensuring it remains self-correcting.

---

## What This Is (and Is Not)

This is a design pattern / methodology for building LLM-driven tools and workflows.

It is not:
- a library or framework
- a model benchmark
- a prompting cookbook
- dependent on any specific vendor or model

It is compatible with both human-in-the-loop and fully automated workflows.

---

## Repository Structure

- `pattern.md` — the canonical definition of the loop
- `philosophy.md` — the underlying mental model and rationale
- `examples/` — applied workflows (patching, diagnosis, planning)
- `comparisons/` — common failure modes and why one-shot prompting is brittle

You can adopt the entire loop, or just individual phases, depending on your needs.

---

## License

MIT License — use freely, adapt as needed.
