# Usage Guide

This guide explains how to use the packaged `relationship-map-maintenance` skill after installation.

## Runtime Order

Treat the packaged skill as a routed workflow, not as a monolithic manual.

1. Read `SKILL.md`.
2. Let it classify the round as `use`, `update`, or `maintain`.
3. Choose the lightest safe read mode: `skip`, `light`, or `full`.
4. Read only the routed support file(s):
   - `10_relationship_map_runtime_protocol.md`
   - `11_relationship_map_execution_contract.md`
   - one low-frequency sidecar or rare-path reference only when needed

The packaged skill is designed so the main `SKILL.md` stays focused on runtime routing, while lower-frequency detail stays off the main path.

## AGENTS As An Index Surface

Treat the project-local `AGENTS.md` block as a durable routing and control surface, not as a place to paste a weak summary copy of the whole workflow.

Use this pattern:

- keep only short durable rules in `AGENTS.md`
- route from `AGENTS.md` into repo-local relationship-map docs only when needed
- when `AGENTS.md` points to a longer document, include explicit `read when` / `skip when` conditions

This keeps always-loaded context small and makes relationship-map routing more predictable.

## Typical Use Cases

Use the skill when:

- a fix or feature likely crosses multiple files, modules, configs, scripts, runtime links, or tests
- the codebase has repeated "fixed one place, forgot another" failures
- the user wants pre-change impact analysis before a non-trivial edit
- the user wants explicit post-change relationship-map updates
- the user wants periodic maintenance or audit of relationship-map artifacts

Skip it when:

- the change is clearly mechanical, local, and relationship-neutral
- a single-file edit has no meaningful upstream or downstream impact
- no reusable relationship artifact would result

## Default Operating Model

Default to project-scoped relationship-map docs:

- `docs/<project-scope>/relationship-map/`

Use `docs/relationship-map/` only when the user explicitly wants one repository-wide relationship-map layer shared across multiple projects or experiments.

Primary paths:

- `use`: pre-change routing and impact analysis
- `update`: refresh only the touched relationship entries after a meaningful change
- `maintain`: periodic or structural upkeep only when needed

Read modes:

- `skip`: no relationship-map reads for clearly local, relationship-neutral changes
- `light`: read `00_index.md` and the minimum relevant shard summary only
- `full`: expand only when the change is high-risk, multi-surface, structurally important, or unresolved by `light`

## Stable Entrypoints

Treat these as stable read-first entrypoints in the repo-local relationship-map layer:

- `00_index.md`
- `10_relationship_map_runtime_protocol.md`
- `11_relationship_map_execution_contract.md`

If one becomes too large, keep the entrypoint filename stable and split below it with second-level routing.

## Initialization And Adoption

Read `initialization-and-adoption.md` only when:

- relationship-map docs do not exist yet
- an existing project must be adopted into this layer
- the current round is changing the relationship-map foundation

Initialization still requires ask-first behavior. Do not silently create relationship-map docs, rewrite unrelated `AGENTS.md` content, or create a new project-local `AGENTS.md` without cause.

## Reading And Non-Reading Cases

To reduce context waste, do not stop at "this file exists." Define when a longer document should and should not be read.

Read a longer protocol or sidecar when:

- the current action enters that document's decision surface
- the main router no longer contains enough detail for a safe next step
- failing to read it would leave routing, freshness, lifecycle, or maintenance judgment under-specified

Skip it when:

- the round is pure chat or light brainstorming
- the current action has not yet entered that protocol's responsibility surface
- the main routing file is already sufficient for the immediate next action

This is why the packaged relationship-map skill uses explicit `read when` / `skip when` sections across its support protocols and sidecars.

## Conservative Maintenance

Relationship-map artifacts are a maintained reference layer, not the source of truth.

- current code, configs, scripts, tests, and runtime artifacts remain implementation reality
- authoritative governance docs remain higher authority for intended behavior and accepted decisions
- when drift is found, refresh the affected map in the same workstream instead of leaving the conflict implicit

Do not silently perform structural changes such as archive, supersede, split, merge, or deletion review transitions without notifying the user.

## Example Prompts

- `Use $relationship-map-maintenance to route this multi-file fix and load only the minimum required relationship-map docs.`
- `Use $relationship-map-maintenance to update the touched critical chain and impact shard after this config-plus-code change.`
- `Use $relationship-map-maintenance to initialize a project-scoped relationship-map layer for slug checkout-refactor.`
- `Use $relationship-map-maintenance to audit stale relationship-map shards and report only material findings.`
