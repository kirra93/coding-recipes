---
name: async-reliability
description: Use when correctness depends on asynchronous or long-running execution semantics such as queues, jobs, retries/redelivery, scheduled work, webhooks, cancellation, timeouts, duplicate delivery, or resumable processing. Do not use merely because code uses async/await or performs a normal synchronous request.
---

# Async reliability

Use this skill to define what happens when asynchronous work is delayed, duplicated, retried, interrupted, or partially completed.

## Workflow

1. **Model durable state.** Identify the source of truth, operation/job identity, meaningful states, terminal states, and ownership.
2. **Define delivery/execution semantics.** State what can be duplicated, reordered, delayed, lost, or resumed. Do not assume exactly-once execution unless the infrastructure truly provides it end to end.
3. **Design idempotency where duplicates are possible.** Define the key/scope, durable effect guard, duplicate response/no-op behavior, and retention if relevant.
4. **Classify failures.** Separate retryable, terminal, and ambiguous outcomes. Define attempts/backoff/dead-letter or terminal handling only as needed.
5. **Define time and cancellation semantics.** Cover step/operation deadlines, cancellation persistence/checkpoints, partial work, and terminal state when relevant.
6. **Make it observable.** Use stable operation/correlation identity and enough status, attempts, timing, progress, and error context to diagnose failures without leaking secrets.
7. **Verify failure paths.** Test duplicate delivery, retry after partial success, timeout/cancellation, restart/recovery, or ordering only where the workflow can experience them.

For complex flows, read `references/reliability-checklist.md` selectively.

## Output

- async flow and source of truth;
- delivery/duplication assumptions;
- idempotency strategy;
- retry/terminal-failure policy;
- timeout/cancellation behavior;
- observability;
- failure-path tests and residual risks.

## Guardrails

- Never add retries without considering duplicated side effects.
- Do not hide permanent failures behind indefinite retries.
- Do not rely on in-memory state for correctness across process restarts.
- A successful enqueue/publish is not proof of successful completion.
