---
name: implementation-planning
description: Use when the user explicitly asks for an implementation plan, or when a change spans multiple meaningful modules/steps and has non-obvious sequencing, dependencies, rollout, migration, or verification constraints. Do not use for routine single-area changes whose implementation path is already clear.
---

# Implementation planning

Use this skill to turn an already-understood change into a short, executable sequence. It is not a second discovery pass or architecture document.

## Workflow

1. **Reuse established findings.** Start from current-task exploration, architecture decisions, and project context. Do not repeat repository-wide discovery.
2. **Resolve only blocking gaps.** Inspect additional code/docs only when a missing detail materially changes sequencing or implementation.
3. **Identify the real change surface.** Include only affected modules, contracts, persisted state, configuration, tests, documentation, deployment, and runtime surfaces that matter to this task.
4. **Order by dependency and safety.** Put prerequisite contract/schema/state changes before dependent behavior when required. Account for rollout overlap or backward compatibility only when relevant.
5. **Split into reviewable steps.** Prefer the smallest steps that can be implemented and verified independently without creating unnecessary temporary abstractions.
6. **Attach verification to risky steps.** State the narrowest useful evidence for each step; widen checks only when blast radius justifies it.
7. **Separate follow-up work.** Keep optional cleanup, future improvements, and adjacent refactors out of the implementation path.

## Output

Keep the plan concise and directly actionable:

1. Goal and assumptions
2. Affected areas
3. Ordered implementation steps
4. Verification points
5. Rollout / migration / compatibility notes, if relevant
6. Risks and dependencies
7. Explicitly out of scope items, when useful

## Guardrails

- Do not create a plan merely because the task is described as "non-trivial".
- Do not repeat discovery already completed by another agent or earlier in the same task.
- Do not invent phases or abstractions to make a plan look comprehensive.
- Do not turn implementation planning into architecture redesign.
- Prefer a minimal vertical slice when it can safely deliver the requested outcome.
