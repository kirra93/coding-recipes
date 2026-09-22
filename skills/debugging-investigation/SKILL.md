---
name: debugging-investigation
description: Use when the root cause of incorrect, intermittent, regressed, integration, concurrency, or performance behavior is not yet known and the task requires investigation before a safe fix. Do not use when a clear compiler/test error already identifies an obvious local correction.
---

# Debugging investigation

Use this skill to move from symptom to evidence-backed root cause before changing behavior blindly.

## Workflow

1. **Define the symptom precisely.** Record expected vs observed behavior, environment/version, frequency, first known occurrence, and what evidence is actually available.
2. **Establish reproducibility.** Find the smallest reliable reproduction or, for intermittent failures, the strongest observable signature and triggering conditions.
3. **Locate the causal path.** Use indexed/code discovery, logs/traces, tests, recent changes, and runtime state to narrow where the observed outcome can be produced. Distinguish symptom location from cause location.
4. **Form a small hypothesis set.** Rank plausible causes by evidence and likelihood. Each hypothesis must predict something observable that differs from the others.
5. **Run the cheapest discriminating test.** Prefer one targeted observation or experiment that eliminates hypotheses over broad speculative instrumentation or multiple simultaneous code changes.
6. **Confirm root cause.** Before a permanent fix, establish a coherent causal chain from trigger/input/state through the faulty behavior to the symptom. If certainty is impossible, state the remaining uncertainty explicitly.
7. **Fix the cause, not the symptom.** Make the smallest change that removes the causal defect without masking unexplained behavior.
8. **Prove the regression is gone.** Add or run a focused regression test/reproduction, then widen verification according to blast radius.

For difficult investigations, read `references/investigation-techniques.md` selectively.

## Output

- symptom and reproduction/signature;
- evidence gathered;
- hypotheses considered and eliminated;
- confirmed or best-supported root cause;
- fix rationale;
- regression verification;
- remaining uncertainty.

## Guardrails

- Do not "fix" unexplained failures with sleeps, retries, catch-all exceptions, null suppression, or larger timeouts unless evidence shows that behavior is the correct solution.
- Avoid changing several causal variables at once when an isolated experiment is practical.
- Do not confuse correlation with causation.
- Instrumentation should answer a specific hypothesis, not generate logs for their own sake.
