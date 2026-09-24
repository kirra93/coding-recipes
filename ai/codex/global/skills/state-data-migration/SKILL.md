---
name: state-data-migration
description: Use when changing persisted or versioned state: database schema/constraints/indexes, stored enums/statuses, cache or local-storage formats, event payload persistence, backfills, imports, or state lifecycle. Do not use for routine CRUD when persisted shape and semantics stay unchanged.
---

# State and data migration

Use this skill to keep persisted state compatible, recoverable, and operationally safe.

## Workflow

1. **Identify the source of truth and owners.** Separate durable state from cache, projections, indexes, derived views, and transient transport payloads.
2. **Define the semantic state change.** Describe old and new shape/lifecycle/invariants, not just the migration syntax.
3. **Check compatibility.** Consider old data with new code and, when deployments overlap, new data with old code. Pay special attention to defaults, nullability, enum/status semantics, serialization, and constraints.
4. **Choose rollout strategy.** Prefer incremental expand → migrate/backfill → contract when compatibility or uptime requires it. Do not force this sequence when a simpler atomic migration is genuinely safe.
5. **Design backfill/import behavior if needed.** Make retries and partial completion safe; define batching, checkpointing, idempotency, and observability proportional to data volume and risk.
6. **Assess operational risk.** Consider locking, table/index rewrite cost, data volume, replication/load effects, rollback/roll-forward options, and deployment order where relevant.
7. **Prove integrity.** Define migration checks, invariants, representative queries/tests, and post-deploy verification.

For non-trivial migrations, read `references/migration-checklist.md` selectively.

## Output

- state/data affected and source of truth;
- old → new semantics;
- compatibility and rollout plan;
- backfill/import plan if any;
- integrity/index/constraint implications;
- rollback or roll-forward strategy;
- verification and operational risks.

## Guardrails

- Do not treat cache or an index as the source of truth unless the project explicitly does.
- Do not assume stored enum/status values can be renamed freely.
- Do not add indexes without a concrete query/integrity reason.
- Destructive or irreversible changes require explicit awareness and a safe rollout story.
