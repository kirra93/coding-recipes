# Global Codex Engineering Guide

## Purpose

Use these instructions as stack-agnostic defaults for software-engineering work across repositories.

Keep repository-specific architecture, commands, frameworks, conventions, documentation standards, and workflows in the repository's own `AGENTS.md`, nested `AGENTS.md`, docs, scripts, task runners, or project skills.

## Instruction scope

- Follow the active instruction hierarchy provided by Codex and the user's current request.
- Within repository instructions, prefer the most specific applicable instruction. Nested `AGENTS.md` files may refine or override broader repository and global defaults.
- Treat project code, project instructions, and project-owned documentation as the source of truth for project behavior.
- If project documentation and code materially disagree, do not silently guess. Identify the conflict and resolve it within the task scope.

## Match process to task size

Do not force a heavyweight workflow onto simple work.

For trivial, well-scoped changes:
- inspect the relevant code;
- make the smallest correct change;
- run the narrowest useful verification;
- report the result.

For non-trivial work:
1. Understand the requested outcome and current behavior.
2. Inspect only the relevant code, instructions, tests, contracts, and docs.
3. Make design decisions only where a meaningful choice exists.
4. Form a short implementation plan when sequencing or risk warrants one.
5. Implement the smallest safe change.
6. Verify from narrow checks outward.
7. Review the changed behavior and directly affected boundaries.
8. Update documentation only when the change makes it necessary.

Ask for clarification only when an unresolved ambiguity materially changes the implementation and cannot be resolved from available project context.

## Scope and context discipline

- Prefer targeted discovery over broad repository scans.
- Do not preload, summarize, or rewrite unrelated files.
- Reuse findings already established in the current task instead of repeating discovery.
- Prefer one minimal vertical slice over a broad multi-area rewrite.
- Do not solve adjacent problems unless they are required for the requested outcome.
- Avoid opportunistic refactors.
- If scope expands materially, keep the current change safe and identify follow-up work separately.
- Treat generated files as generated; modify their source or generator unless the project explicitly says otherwise.

## Tool output discipline

Keep tool output targeted and reusable.

- Prefer narrow searches, bounded reads, and focused command output over dumping whole files, logs, test suites, or directory trees.
- When command output can be large, filter it at the source with targeted paths, patterns, line ranges, `head`, `tail`, or equivalent options.
- Reuse results already gathered in the current task instead of repeating equivalent reads or searches.
- Do not repeatedly run broad repository scans or the same verification command unless new evidence requires it.
- For verbose test/build/log output, capture the full output to a file when useful and inspect only the relevant failure or summary sections.

## Engineering defaults

- Prefer simple, explicit designs over speculative abstraction.
- Follow existing project architecture and conventions before introducing new patterns.
- Use SOLID, patterns, DDD, Hexagonal/Clean Architecture, repositories, factories, strategies, adapters, and similar techniques only when they solve a concrete problem or protect a meaningful boundary.
- Keep responsibilities cohesive and dependencies explicit.
- Keep framework, transport, UI, and infrastructure glue thin when the existing architecture supports it.
- Keep business rules testable where practical.
- Make side effects and ownership clear.
- Preserve public and persisted contracts unless a breaking change is explicitly requested.
- Preserve backward compatibility when practical and required by the project.
- Prefer deterministic behavior for tests and reproducible workflows.
- Prefer idempotent behavior for retryable or duplicate-prone operations when relevant.
- Do not introduce a production dependency without a concrete benefit and awareness of its operational cost.
- Never hard-code real secrets, credentials, machine-specific paths, or environment-specific values into source.
- Do not perform destructive repository, filesystem, database, or infrastructure operations unless they are explicitly requested or clearly required by the task.

## Verification

- Discover verification commands from project instructions, scripts, CI, task runners, and existing conventions.
- Run the narrowest relevant checks first.
- Expand to broader tests, linting, type checks, builds, migrations, integration checks, or runtime verification only when the affected scope warrants it.
- Do not claim a check passed unless it actually ran and passed.
- When a check cannot be run, state what was not verified and provide the exact project-specific command when known.
- Treat failing existing checks separately from regressions introduced by the current change.

## Documentation and comments

- Follow the project's documentation structure and terminology.
- Update documentation when the task changes public behavior, setup, configuration, contracts, persisted data, deployment/operations, or another documented source of truth.
- Do not create or rewrite documentation merely to satisfy a generic process step.
- Prefer one canonical source of truth over duplicated documentation.
- Comments and doc comments should explain purpose, constraints, invariants, side effects, lifecycle, or non-obvious reasoning.
- Do not add comments that merely restate readable code.

## Skills

- Use a skill only when the current task matches its trigger and the specialized workflow adds value.
- Do not load skills merely because they are available or vaguely related.
- Prefer repository-specific skills for repository-specific workflows and domain knowledge.
- Reuse skill outputs and prior findings instead of repeating the same investigation in another workflow.

## Subagents

Use subagents only when delegation reduces uncertainty, parallelizes independent read-only work, or adds a genuinely different review perspective.

- Do not delegate trivial work.
- Prefer read-only delegation for exploration, research, architecture analysis, and review.
- Keep delegated scopes narrow and give each subagent a clear stopping condition.
- Reuse subagent findings; do not have later agents repeat repository-wide discovery.
- Do not run multiple write-capable agents against the same files concurrently.
- Use specialized security review only for changes that cross a meaningful security or trust boundary.
- Prefer a focused diff review over a broad repository audit after implementation.

## Codebase discovery tools

When a codebase knowledge graph or indexer is available and current:
- prefer it for symbol discovery, call relationships, and high-level navigation;
- use direct file reads to verify implementation details before changing code;
- fall back to native search for string literals, errors, configuration, non-code files, generated artifacts, or incomplete/stale index results.

The repository contents remain the source of truth when an index and the current files disagree.

## Completion

For implementation tasks, finish with a concise summary of:
- what changed;
- what was verified;
- anything important that could not be verified;
- remaining material risks or follow-up work, if any.

Do not produce ceremony, long plans, or exhaustive checklists when the task does not need them.

<!-- codebase-memory-mcp:start -->
# Codebase Knowledge Graph (codebase-memory-mcp)

This project uses codebase-memory-mcp to maintain a knowledge graph of the codebase.
ALWAYS prefer MCP graph tools over grep/glob/file-search for code discovery.

## Priority Order
1. `search_graph` — find functions, classes, routes, variables by pattern
2. `trace_path` — trace who calls a function or what it calls
3. `get_code_snippet` — read specific function/class source code
4. `query_graph` — run Cypher queries for complex patterns
5. `get_architecture` — high-level project summary

## When to fall back to grep/glob
- Searching for string literals, error messages, config values
- Searching non-code files (Dockerfiles, shell scripts, configs)
- When MCP tools return insufficient results

## Examples
- Find a handler: `search_graph(name_pattern=".*OrderHandler.*")`
- Who calls it: `trace_path(function_name="OrderHandler", direction="inbound")`
- Read source: `get_code_snippet(qualified_name="pkg/orders.OrderHandler")`
<!-- codebase-memory-mcp:end -->
