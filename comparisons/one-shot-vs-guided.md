# One-Shot Prompting vs Guided Convergence

## One-Shot Prompting

A one-shot approach asks for a complete answer in a single generation.

Typical strengths:
- fast when it works
- low integration effort

Typical failure modes:
- errors compound silently
- large, unnecessary edits (“overreach”)
- plausible but incorrect reasoning (“hallucinated coherence”)
- poor debuggability (no intermediate artifacts)
- brittle to ambiguity and missing context

## Guided Convergence

Guided convergence decomposes the task into phases with explicit constraints and critique.

Typical strengths:
- stable, inspectable intermediates
- easier to enforce minimality
- supports objective validation (tests/builds)
- works better with smaller/cheaper models
- safer in high-precision tasks (patching, planning)

Typical costs:
- more prompts (but often fewer failed attempts)
- requires orchestration logic and checks
- demands clear acceptance criteria

## Practical Guidance

Prefer guided convergence when:
- correctness matters
- outputs must be minimal
- the task is multi-step
- failure needs to be diagnosable
- you are using smaller models

One-shot can be fine when:
- the task is low risk
- you can easily verify the result
- the output is disposable or exploratory
