---
name: architecture-design
description: Use when a task requires a non-obvious architectural choice affecting ownership, module/service boundaries, lifecycle, cross-cutting data flow, or long-term extensibility. Do not use for routine implementation that follows an established project pattern.
---

# Architecture design

Use this skill to make a concrete architectural decision, not to decorate routine work with architecture terminology.

## Workflow

1. **State the decision.** Identify the architectural question that is actually open. If there is no meaningful choice, follow the established project pattern and stop using this skill.
2. **Establish constraints.** Reuse current-task findings first. Inspect only the code/docs needed to confirm ownership, existing boundaries, invariants, deployment/runtime constraints, and compatibility requirements.
3. **Define ownership and boundaries.** Decide which component owns the behavior, where state lives, what crosses a boundary, where side effects happen, and which dependencies must remain one-way.
4. **Describe lifecycle and failure behavior.** Cover creation/transition/completion/failure/cleanup only where relevant. Include retries, cancellation, persistence, or concurrency only if the design actually involves them.
5. **Compare meaningful alternatives.** Usually two or three are enough. For each, state the concrete benefit, cost, and risk. Do not invent alternatives merely to make the analysis look thorough.
6. **Choose the smallest durable design.** Prefer a solution that fits current conventions and solves the requested problem without speculative extension points.
7. **Identify consequences.** Note affected contracts, persisted state, async behavior, security boundaries, rollout concerns, and verification needs only when they materially change.

For a deep architecture review, read `references/design-checklist.md` selectively rather than applying every item automatically.

## Output

Keep the result concise:
- decision to make;
- relevant current constraints;
- chosen design and ownership/boundaries;
- meaningful alternatives rejected;
- material risks and downstream implications;
- verification/rollout notes.

## Guardrails

- Project architecture and current code outrank generic architecture recipes.
- Do not introduce a named pattern unless it solves a concrete problem or protects a meaningful boundary.
- Do not redesign adjacent areas to make the chosen design look cleaner.
- Treat unresolved assumptions that could change the design as explicit risks.
