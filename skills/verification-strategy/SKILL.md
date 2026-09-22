---
name: verification-strategy
description: Use when a non-trivial change needs a deliberate, risk-based verification plan across tests, contracts, migrations, builds, runtime checks, or manual evidence. Do not use merely to remind the agent to run an obvious focused check for a trivial edit.
---

# Verification strategy

Use this skill when choosing *what evidence is enough* is itself non-trivial.

## Workflow

1. **Identify changed behavior and failure risk.** Map the patch to observable behavior, affected boundaries, state, and important failure modes.
2. **Choose the cheapest discriminating checks first.** Prefer a focused unit/module/contract/integration check that directly proves the change over a broad suite that merely produces activity.
3. **Widen only for justified blast radius.** Add broader suite/build/type/lint/e2e/migration/runtime checks when shared infrastructure, cross-module contracts, generated artifacts, deployment behavior, or risk warrants them.
4. **Cover negative and transition paths.** For non-trivial behavior, verify relevant invalid input, permission/error handling, compatibility, migration, retry/idempotency, or state transitions rather than only the happy path.
5. **Record actual evidence.** Distinguish checks that ran and passed from checks not run, blocked, flaky, or already failing for unrelated reasons.
6. **State residual risk.** If the environment cannot prove an important property, say what remains uncertain and how to verify it.

## Output

- behavior/risk being verified;
- checks run or proposed, from narrow to broad;
- what each check proves;
- results and unrelated pre-existing failures;
- unverified properties and residual risk.

## Guardrails

- Do not equate a green broad suite with proof of an untested behavior.
- Do not claim a command ran if it did not.
- Do not turn verification into unrelated cleanup.
- Prefer useful partial evidence over fabricated confidence.
