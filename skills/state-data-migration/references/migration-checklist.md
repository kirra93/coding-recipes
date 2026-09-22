# Migration deep checklist

Use only relevant sections.

## Compatibility
- Old rows/documents/messages readable by new code
- New writes readable by old code during overlap
- Default/null/backfill semantics
- Stored enum/status compatibility
- Serialization/version compatibility

## Rollout
- Single atomic deployment safe?
- Expand/migrate/contract needed?
- Read-path before write-path changes?
- Feature flag or dual-read/write needed?
- Rollback versus roll-forward preference

## Backfill
- Batching and rate limiting
- Checkpoint/resume behavior
- Idempotency
- Failure recording
- Progress/metrics
- Verification of completeness

## Database/operational
- Lock duration
- Table/index rewrite
- Constraint validation strategy
- Concurrent index creation where supported
- Replication/storage/load impact
