# Async reliability deep checklist

Use only applicable items.

## Identity and state
- Operation/job/event identifier
- Correlation/causation identifier
- Durable status/stage
- Terminal success/failure/cancel states
- Ownership of state transitions

## Delivery
- At-most-once / at-least-once / best-effort characteristics
- Duplicate delivery
- Reordering
- Delayed delivery
- Poison messages
- Consumer crash after side effect but before acknowledgement

## Idempotency
- Key and scope
- Durable uniqueness/guard
- External side-effect idempotency support
- Duplicate response/result behavior
- Retention/expiry of idempotency records

## Retry and time
- Retryable vs terminal failures
- Ambiguous external timeouts
- Backoff/jitter
- Max attempts / dead-letter behavior
- Per-step and whole-operation deadlines

## Recovery and observability
- Restart/resume behavior
- Checkpoints
- Progress/heartbeat
- Attempt count and last error
- Metrics for age, failures, retries, stuck work
