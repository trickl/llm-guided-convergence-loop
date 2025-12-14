# LLM Guided Convergence Loop

A practical methodology for working with large language models (LLMs) when correctness,
minimality, and reliability matter more than one-shot convenience.

This repository documents a simple but powerful idea: **LLM outputs should be treated as
provisional artifacts that improve through guided iteration**, not as final answers
generated in a single prompt.

---

## Why This Exists

If you have ever experienced any of the following:

- LLM-generated patches that almost work, but subtly break things
- Large, unfocused diffs when you asked for a small fix
- Plausible explanations that collapse under closer inspection
- Strong results from flagship models, followed by poor results from smaller ones
- Difficulty understanding *why* a model produced a particular answer

…then this repository is for you.

The core problem is not model quality.  
It is the **mental model** most people use when interacting with LLMs.

### The One-Shot Fallacy

Many failures stem from asking an LLM to do too much at once:

> “Here is the error and the code. Fix it.”

This forces the model to simultaneously:
- interpret the problem,
- locate the cause,
- decide on a fix,
- apply constraints implicitly,
- and emit a formally correct artifact.

Errors compound silently, and debugging becomes guesswork.

### What This Pattern Changes

The Guided Convergence Loop replaces one-shot prompting with **explicit, inspectable steps**.
It externalises reasoning that is often hidden inside advanced “reasoning models” and makes
it usable, debuggable, and reliable — even with smaller or cheaper models.

This turns LLMs from brittle answer generators into **collaborative components in a
controlled process**.

---

## What This Helps With

The Guided Convergence Loop is especially useful for tasks where precision matters:

- Fixing compiler or runtime errors with minimal patches
- Generating diffs that must apply cleanly
- Diagnosing failures before changing code
- Planning multi-step engineering work
- Building LLM-driven tools that must be reliable, testable, and cost-efficient

It is less about creativity, and more about **engineering discipline** applied to LLMs.

---

## The Loop

The pattern is an explicit sequence of phases:

1. **Interpret** — explain what the input means (e.g., an error message or requirement).
2. **Propose** — generate an initial candidate solution, often in prose.
3. **Constrain** — apply explicit scope, format, and correctness constraints.
4. **Critique** — evaluate the proposal against constraints and objective signals.
5. **Refine** — revise the artifact to address critique with minimal additional change.
6. **Converge** — repeat until acceptance criteria are met or failure is diagnosed.

Each phase reduces uncertainty and makes the next step safer.

---

## What This Is (and Is Not)

- This is a **design pattern / methodology** for LLM-driven systems.
- It is **not** a framework, SDK, or prompting cookbook.
- It does not depend on any specific model or vendor.
- It is compatible with human-in-the-loop and fully automated workflows.

The emphasis is on **process design**, not prompt cleverness.

---

## How to Use This Repository

- Read **[pattern.md](pattern.md)** for the formal definition of the loop.
- Read **[philosophy.md](philosophy.md)** for the underlying mental model.
- Explore **[examples/](examples/)** for concrete, task-oriented workflows.
- See **[comparisons/](comparisons/)** for why one-shot prompting is brittle in practice.

You can adopt the entire loop, or just individual phases, depending on your needs.

---

## License

MIT License — use freely, adapt as needed.
