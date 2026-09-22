# Debugging investigation techniques

Choose techniques based on the hypothesis; do not apply all of them.

## Reproduction and minimization
- Reduce input/state/environment until the failure just persists
- Compare known-good and known-bad cases
- Capture deterministic seeds, timestamps, versions, or fixtures when relevant

## Change localization
- Inspect recent relevant diffs
- Bisect when there is a reliable regression signal
- Compare configuration/dependency/runtime versions

## Data/control-flow evidence
- Trace callers/callees and state transitions
- Inspect boundary inputs/outputs
- Add temporary structured logging around a specific hypothesis
- Use traces/profilers when timing/concurrency/performance is causal

## Concurrency/intermittent failures
- Identify shared mutable state and ownership
- Check ordering assumptions, races, locks, atomicity, cancellation, and retries
- Record operation/correlation IDs and timing
- Prefer stress/repeat tests that preserve a failure signature

## Data/storage failures
- Compare persisted state before/after the triggering operation
- Check transaction boundaries and isolation assumptions
- Inspect migration/version compatibility
- Verify cache/index/projection freshness separately from source-of-truth data

## Performance anomalies
- Measure before optimizing
- Separate latency, throughput, allocation/memory, I/O, database, lock, and external-service contributors
- Profile the hot path rather than guessing from code appearance
