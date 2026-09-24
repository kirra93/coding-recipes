# Global Codex skills — final minimal set

This package contains the recommended **user-global** skills after moving permanent engineering defaults into the global `AGENTS.md` and leaving repository-specific workflows and documentation standards to project-level instructions/skills.

## Install

Copy the eight directories under `skills/` to:

```text
~/.agents/skills/
```

Recommended final global set:

```text
architecture-design/
async-reliability/
contract-boundary-design/
debugging-investigation/
implementation-planning/
security-review/
state-data-migration/
verification-strategy/
```

## Intentionally not global

- `problem-framing` — its useful defaults belong in global `AGENTS.md`; project-specific framing belongs near the project.
- `documentation-standard` — your documentation standard is supplied per project, so a global fallback would create another competing source of truth.

## `implementation-planning` trigger

Use it when:
- the user explicitly asks for an implementation plan;
- a change spans multiple meaningful modules or steps;
- sequencing/dependencies are non-obvious;
- rollout, migration, compatibility, or staged verification matters.

Do **not** use it for a routine local change whose implementation path is already clear.

It must reuse existing explorer/architect/current-task findings and must not repeat repository discovery.

## Design rules used in this package

- Each skill has a narrow positive trigger and an explicit non-trigger.
- `SKILL.md` contains specialized workflow, not generic engineering policy already present in global `AGENTS.md`.
- Deep checklists live in `references/` and are read only when the task warrants them.
- Skills do not hard-code agent names, models, MCP tool names, or repository commands.
- A routine task may legitimately use **zero** custom skills.

## Migration

1. Back up your current `~/.agents/skills/`.
2. Replace the eight included skill directories.
3. Remove old global `problem-framing/` and `documentation-standard/` if present.
4. Keep unrelated system/vendor/project skills untouched.
5. Start a new Codex session so skill discovery metadata is refreshed.
