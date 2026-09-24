---
name: contract-boundary-design
description: Use when changing the shape or semantics of a consumed boundary such as an API, DTO, event/message, exported interface, storage format, or frontend/backend contract, especially when compatibility matters. Do not use for purely internal refactors with no observable contract change.
---

# Contract and boundary design

Use this skill to make boundary semantics explicit and compatible.

## Workflow

1. **Identify the contract.** Name the producer/owner, consumers, boundary type, stability expectations, and source of truth.
2. **Describe the semantic change.** Focus on meaning, not just fields: required/optional values, defaults, nullability, enum semantics, validation, ordering, idempotency, pagination, or error behavior.
3. **Check compatibility.** Evaluate old consumer ↔ new producer and new consumer ↔ old producer when rollout can overlap. State clearly whether the change is additive, conditionally compatible, or breaking.
4. **Define failure semantics.** Specify validation failures, public-safe errors, retryability where relevant, and how internal failures map across the boundary.
5. **Choose rollout/versioning only if needed.** Prefer the simplest compatible path. Add versioning, dual support, or deprecation only when consumers or rollout constraints justify it.
6. **Define proof.** Identify the smallest contract/integration/compatibility tests and documentation/schema updates needed to keep the contract authoritative.

For complex compatibility work, read `references/compatibility-checklist.md` selectively.

## Output

- contract and consumers;
- semantic changes;
- compatibility result;
- validation/error behavior;
- rollout/versioning implications;
- tests and canonical docs/schema to update.

## Guardrails

- Do not change a consumed contract silently.
- Do not expose internal implementation details merely because they are convenient to serialize.
- Treat undocumented-but-relied-upon behavior as a compatibility risk, not automatically as permission to break it.
- Avoid versioning when a safe additive change is sufficient.
