# Philosophy and Mental Model

## The Central Claim

LLMs are not compilers, solvers, or proof systems. They are probabilistic generators that can be extraordinarily useful when embedded in a process that:

- reduces ambiguity,
- enforces constraints,
- validates outputs,
- and iterates toward correctness.

The Guided Convergence Loop treats the LLM as a **component** in a larger reasoning system, rather than as the system itself.

## Why One-Shot Prompting Fails

One-shot prompting commonly fails because it asks the model to do too much at once:

- interpret the problem,
- identify the root cause,
- choose a fix,
- locate the change,
- implement the change,
- keep it minimal,
- and emit a formally correct artifact.

Each step contains uncertainty. When combined in a single generation, uncertainty compounds.

## Why Iteration Works

Iteration works because it serialises uncertainty:

- early steps reduce entropy (interpretation, localisation),
- constraints stabilise outputs (scope, format, minimality),
- critique finds mismatches cheaply,
- refinement edits rather than rewrites,
- convergence is measured by objective acceptance criteria.

## Opaque vs Explicit Reasoning

Some high-end models appear to “just work” because they likely perform internal refinement loops. This can create a misconception for beginners: when a smaller model fails, it can look like the model is the problem, when the real issue is the missing process.

The goal of this repository is to make that process explicit and reusable.

## Design Principles

- **Make intermediate artifacts visible**: proposals, critiques, constraints, deltas.
- **Prefer mechanical translations late**: once the intent is stable, generate diffs/code.
- **Enforce minimality**: large changes reduce debuggability and increase risk.
- **Instrument everything**: apply checks early and often.
- **Fail clearly**: if convergence does not happen, emit a diagnosis that helps a human intervene.
