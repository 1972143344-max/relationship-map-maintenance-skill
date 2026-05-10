---
name: relationship-map-maintenance
description: Create and maintain project-scoped relationship and impact maps for complex code changes. Use when fixing bugs across multi-file call chains, tracing dependencies beyond imports, updating explicit change-impact shards, auditing relationship-map changes, or periodically checking whether curated relationship maps are stale, incomplete, conflicting, or ready for deletion review. If this skill is adopted as the governing workflow for the current action, read the full main SKILL.md before major relationship-map routing, update, or maintenance actions.
---

# Relationship Map Maintenance

Use this skill to operate a project-scoped relationship-map layer without letting relationship maps replace code, governance, tests, or review.

Default to `docs/<project-scope>/relationship-map/`.
Use `docs/relationship-map/` only when the user explicitly wants one repository-wide relationship-map layer shared across multiple projects or experiments.

## G0. Front Door

### Use This Skill When

- the user asks to build or maintain dependency, relationship, impact, or call-chain maps
- a bug fix or feature likely crosses multiple files, modules, configs, scripts, runtime links, or tests
- the codebase has repeated "fixed one place, forgot another" failures
- the user wants pre-change impact analysis or post-change relationship-map updates for a non-trivial edit
- the user wants periodic maintenance of relationship maps through automation

### Do Not Use This Skill When

- the change is clearly mechanical, local, and relationship-neutral
- a single-file edit has no meaningful upstream or downstream impact
- the relevant change surface is already obvious and no reusable relationship artifact would result
- the user only wants ordinary code changes and no explicit relationship-map workflow is needed

### First Step After Trigger

Once this skill is adopted as the governing workflow for the current action:

1. read this main `SKILL.md`
2. classify the round as `use`, `update`, or `maintain`
3. choose the lightest safe mode: `skip`, `light`, or `full`
4. route only into the support protocol or sidecar actually needed

Do not jump straight into initialization, audit, automation, or deletion detail unless the current action actually needs that path.

### Relationship-Map Truth Boundary

Relationship-map artifacts are a maintained reference layer, not the source of truth.

- current code, runtime files, configs, scripts, tests, and artifacts remain implementation reality
- authoritative governance docs remain higher authority for intended behavior, constraints, and decisions
- if current code or authoritative governance docs conflict with a relationship map, code and governance win
- when such drift is discovered, refresh the affected map in the same workstream instead of leaving the conflict implicit

### Structural Change Boundary

Do not silently change what future agents will read first.

This includes:

- archive or supersede actions
- structural shard changes such as merge or split
- deletion review or approved deletion
- AGENTS-block adoption that changes persistent routing behavior

## G1. Runtime Routing

This main file is a runtime router, not the whole manual.

Use it to determine which support protocol or low-frequency sidecar must be read next.

### Read `10_relationship_map_runtime_protocol.md`

Read `10_relationship_map_runtime_protocol.md` when the current round involves:

- non-trivial repo work that depends on relationship-map reading quality
- choosing `skip`, `light`, or `full`
- deciding between `00_index.md`, shard summaries, shard bodies, generated manifest, or generated artifacts
- relationship-map routing, probing, or read-budget judgment

Skip `10_relationship_map_runtime_protocol.md` when the round is:

- pure chat
- light brainstorming with no repo-document lookup
- a clearly `skip`-eligible local change where no relationship-map read is needed

### Read `11_relationship_map_execution_contract.md`

Read `11_relationship_map_execution_contract.md` when the current round involves:

- relationship-map shard or index updates
- freshness-state changes
- audit-log updates
- maintenance reports
- structural changes such as archive, supersede, split, merge, or deletion review
- review-threshold or closure judgment for relationship-map modifications

Skip `11_relationship_map_execution_contract.md` when the round is:

- pure chat
- read-only routing with no relationship-map modification or sync decision
- a clearly `skip`-eligible code change that does not touch relationship-map artifacts

### Read Low-Frequency Sidecars

Route to these only when the action actually needs them:

- `initialization-and-adoption.md` for first-time setup or project adoption
- `relationship-map-surface-catalog.md` for the full document set, stable entrypoints, or template routing
- `references/conflict-lifecycle-and-deletion.md` for shard conflict, lifecycle, archive, supersede, or deletion handling
- `references/audit-and-automation.md` for audit minimum set, maintenance runs, or automation guardrails
- `references/automation-workflow.md` for recurring maintenance design

### Main-File-Only Cases

This main file alone is usually enough only when the current action is:

- deciding whether to trigger the skill at all
- classifying the round as `use`, `update`, or `maintain`
- choosing `skip`, `light`, or `full`
- identifying which deeper support file must be read next

## G2. Runtime Operating Model

### Primary Paths

- `use`: pre-change routing and impact analysis
- `update`: post-change freshness or shard updates only when relationship meaning or shard state changed
- `maintain`: periodic or structural upkeep only when actually needed

Do not let maintenance dominate ordinary use of this skill.

### Read Modes

- `skip`: no relationship-map reads for clearly mechanical or relationship-neutral changes
- `light`: read `00_index.md` and the minimum relevant shard summary only
- `full`: expand only when the change is high-risk, multi-surface, structurally important, or unresolved by `light`

### Hard Skip Gate

Use `skip` directly when all of the following are true:

- the change is mechanical, local, and clearly behavior-neutral
- no shared contract, entrypoint, or core config format is touched
- no existing `critical-chain` is touched
- there is no reason to believe shard freshness or relationship meaning changed

### Hard Full Gate

Use `full` directly when any of the following is true:

- `>= 3` files changed
- the change crosses `>= 2` surfaces among code, config, script, tests, artifacts, or relationship-map docs
- an entrypoint, shared contract, or core config format changed
- an existing `critical-chain` was touched
- the expected change-impact checklist would contain `>= 5` follow-up checks
- conflict handling, deletion review, structural shard change, or relationship-map automation is involved

### Lightweight Assessment

If neither hard gate applies, use only these low-cost checks:

- does this change alter an existing relationship description
- does it add a reusable relationship edge
- does it make any current shard stale or partial
- is it touching a historically omission-prone chain

Use `skip` if all answers are no.
Use `light` if one answer is yes and the impact remains local.
Upgrade to `full` if multiple answers are yes or if the answer remains unclear after reading `00_index.md` and one shard summary.

### Reuse-First Rule

Prefer reuse of existing written relationship-map results over repeated analysis.

- if `00_index.md` routes to the right shard, do not scan the whole tree
- if a shard summary answers the routing question, do not open multiple shard bodies
- if a curated shard already captures the needed relationship, do not re-derive it from generated artifacts
- if `generated/00_manifest.md` points to the needed evidence, do not scan the whole `generated/` folder
- if an existing maintenance report already identified the stale or conflicting item, do not repeat the same detection work unless fresh verification is required

Written artifacts should reduce repeated context spend, not create more of it.

### Persistent AGENTS Adoption

This skill has two install surfaces:

1. the project-scoped `docs/<project-scope>/relationship-map/` document layer
2. the project-local `AGENTS.md` persistent rule layer

Treat the `AGENTS.md` block as an index-bearing control surface:

- keep it short and durable
- use it to route into repo-local relationship-map docs
- do not turn it into a weak summary copy of the whole skill

If a project-local `AGENTS.md` already exists, append the relationship-map block incrementally.
Do not rewrite or reorganize unrelated `AGENTS.md` content.

## G3. Structural Control And Closure

### Ask-First

Ask before:

- initializing the relationship-map layer
- adopting an existing project into this layer
- creating a new project-local `AGENTS.md`
- deleting relationship-map artifacts

### Notify-First

Tell the user explicitly before or while performing:

- archive or supersede actions
- merge or split of curated shards
- deletion-candidate transitions that may lead to physical deletion
- changes that materially reorganize relationship-map routing or persistent AGENTS behavior

### Same-Round Sync Rule

Treat shard update plus index update as one documentation action when relationship meaning, freshness, or status changed materially.

Do not leave:

- shard state changed but `00_index.md` stale
- lifecycle state changed but `02_audit_log.md` missing when traceability is required
- structural route changes unreported

### Review Boundary

Relationship maps help drive review. They do not replace review.

Require a review pass for relationship-map-driven work when any of these is true:

- `>= 3` files changed
- the change crosses `>= 2` surfaces among code, config, script, tests, artifacts, or relationship-map docs
- an entrypoint, shared contract, or core config format changed
- the change-impact checklist contains `>= 5` follow-up checks
- an existing `critical-chain` was touched

## G4. Sidecar Routing

### `10_relationship_map_runtime_protocol.md`

- Position: `high-frequency support protocol`
- Description: route-first reading contract for relationship-map routing, read budgets, curated-vs-generated expansion, and stop rules
- Read when:
  - relationship-map reading quality matters for the current task
  - mode selection or document expansion needs more than the main router
- Skip when:
  - the round is pure chat
  - the round is clearly `skip`

### `11_relationship_map_execution_contract.md`

- Position: `high-frequency support contract`
- Description: update, audit, maintenance, structural-notify, and review-threshold rules for relationship-map modifications
- Read when:
  - the round is updating relationship-map docs or making structural decisions
  - audit, maintenance, or deletion-review handling matters
- Skip when:
  - the round is read-only routing with no relationship-map sync decision

### `initialization-and-adoption.md`

- Position: `low-frequency workflow sidecar`
- Description: initialization steps, adoption sequence, AGENTS-block integration, and minimum first-use setup
- Read when:
  - relationship-map docs do not exist yet
  - an existing project must be adopted into this layer
- Skip when:
  - the layer is already established and the current action is not changing its foundation

### `relationship-map-surface-catalog.md`

- Position: `low-frequency routing sidecar`
- Description: full relationship-map document set, stable entrypoints, document roles, and template routing
- Read when:
  - you need the full relationship-map surface set or template map
  - you are changing structure or setting up a new project scope
- Skip when:
  - the current action already has a known protocol or document target

### Rare-Path References

Read only when the action explicitly needs them:

- `references/conflict-lifecycle-and-deletion.md`
- `references/audit-and-automation.md`
- `references/automation-workflow.md`
