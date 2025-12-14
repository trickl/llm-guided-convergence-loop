# LLM Guided Convergence Loop

A practical methodology for working with large language models (LLMs) using explicit, iterative refinement rather than one-shot prompting.

The core idea is simple: treat LLM outputs (plans, patches, analyses, summaries) as *proposals* that improve through constrained iteration. This makes outcomes more reliable, more inspectable, and easier to debug—especially when using smaller or cheaper models.

## The Loop

The Guided Convergence Loop is an explicit sequence of phases:

1. **Interpret** — explain what the input means (e.g., an error message, a requirement, a failing test).
2. **Propose** — generate a first candidate solution or approach (often in prose).
3. **Constrain** — apply requirements, scope limits, format rules, and “minimal change” constraints.
4. **Critique** — evaluate the proposal against constraints and reality (including objective signals).
5. **Refine** — update the proposal to address critique with minimal additional change.
6. **Converge** — repeat until acceptance criteria are met, or fail fast with a clear diagnosis.

This repository documents the pattern, why it works, and how to apply it to common engineering tasks.

## What This Is (and Is Not)

- This is a **design pattern / methodology** for building LLM-driven tools and workflows.
- This is **not** a library, framework, or model benchmark.
- The goal is to make LLM usage more *operationally reliable*, not more “clever”.

## Quick Start

- Read: [pattern.md](pattern.md) for the canonical definition.
- Read: [philosophy.md](philosophy.md) for the mental model and rationale.
- Browse: [examples/](examples/) for applied workflows (patching, diagnosis, planning).
- Compare: [comparisons/](comparisons/) for common failure modes and why one-shot prompting is brittle.

## License

This methodology is distributed under the MIT License.
