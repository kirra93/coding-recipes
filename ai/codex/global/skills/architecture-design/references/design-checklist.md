# Architecture design deep checklist

Use only the sections relevant to the current decision.

## Ownership and boundaries
- Who owns the capability and its source of truth?
- Which dependencies point inward/outward?
- Is there duplicated ownership or hidden coupling?
- Which interfaces are stable contracts versus implementation details?

## State and lifecycle
- Where is state created, validated, persisted, transitioned, and retired?
- Which invariants must hold across transitions?
- What happens on partial failure or restart?
- Are derived state and cache clearly separated from source-of-truth state?

## Failure domains
- Which components can fail independently?
- Does one failure unnecessarily cascade into another boundary?
- Are timeouts/retries/cancellation relevant to this design?

## Change and rollout
- Can the change ship incrementally?
- Does it require compatibility between old/new code or old/new data?
- Is a migration, backfill, feature flag, dual-read/write, or staged rollout required?

## Operability
- What must be observable to diagnose failures?
- Are ownership and support boundaries clear?
- Does the design add a new operational dependency or failure mode?
