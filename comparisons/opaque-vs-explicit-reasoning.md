# Opaque vs Explicit Reasoning Loops

## Opaque Reasoning (Implicit Iteration)

Some models appear to “think” and deliver strong results in a single response. In practice, this often resembles an internal refinement loop that the user cannot directly observe or instrument.

Pros:
- excellent user experience
- fewer visible steps
- strong default performance

Cons:
- reduced observability (hard to know why it worked)
- difficult to replicate on smaller models
- harder to integrate into systems that need explicit checkpoints
- can mislead beginners into attributing success to “model quality” alone

## Explicit Reasoning (Externalised Iteration)

The Guided Convergence Loop externalises the reasoning process into visible steps and artifacts.

Pros:
- debuggable and auditable
- portable across models
- easier to apply quantitative checks
- enables targeted costs (cheap model for critique, etc.)

Cons:
- requires orchestration
- requires discipline in constraints and acceptance criteria

## Practical Takeaway

If you are building tools, prefer explicit loops:
- you can test them,
- measure them,
- and improve them systematically.

Opaque reasoning is convenient at the UI layer, but explicit reasoning is often superior at the systems layer.
