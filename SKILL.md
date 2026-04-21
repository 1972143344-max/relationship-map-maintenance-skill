---
name: relationship-map-maintenance
description: Create and maintain project-scoped relationship and impact maps for complex code changes. Use when fixing bugs across multi-file call chains, tracing dependencies beyond imports, updating explicit change-impact shards, auditing relationship-map changes, or periodically checking whether curated relationship maps are stale, incomplete, conflicting, or ready for deletion review.
---

# Relationship Map Maintenance

Create and maintain a project-scoped relationship and impact layer so multi-file fixes and features do not stop at the first edited file and leave related code, config, scripts, runtime links, or tests stale.

This skill is for explicit change-impact tracking, not for generic prose documentation.

Default to project-scoped relationship maps under `docs/<project-scope>/relationship-map/`.
Use `docs/relationship-map/` only when the user explicitly wants one repository-wide map shared across multiple projects or experiments.

## Quick Path

Use the shortest path that is still safe.

1. Decide whether the task is `skip`, `light`, or `full`.
2. If `skip`, do not open relationship-map docs.
3. If `light` or `full`, route through `00_index.md` first.
4. Read only the minimum shard summary or shard body needed for the current task.
5. Reuse existing written results before re-deriving relationships from scratch.
6. After a meaningful change, update only the touched shard, index, and freshness state that actually changed.
7. Use maintenance, audit, lifecycle, deletion, and automation detail only on the rare path.

Primary path order:

- `use`: pre-change routing and impact analysis
- `update`: post-change freshness or shard updates
- `maintain`: periodic or structural upkeep

Do not let maintenance dominate ordinary use of this skill.

## Use This Skill When

- the user asks to build or maintain dependency, relationship, impact, or call-chain maps
- a bug fix likely crosses multiple files, modules, scripts, configs, or tests
- the codebase has repeated "fixed one place, forgot another" failures
- the user wants change-impact review before or after a non-trivial edit
- the user wants periodic maintenance of relationship maps through automation

## When Not To Trigger

This skill usually does not need to be expanded for:

- single-file mechanical edits with no meaningful upstream or downstream impact
- formatting-only or comment-only changes
- trivial text or naming fixes that do not affect behavior
- narrow local edits where the relevant change surface is already obvious and no reusable relationship artifact would result

## Reference Boundary

This skill is a reference layer, not a substitute for normal engineering analysis.

Do not rely only on the relationship map when implementing or reviewing changes.
Also use the actual code, targeted search, diffs, tests, runtime validation, config checks, and independent review.

The relationship-map layer should reduce omission risk, not narrow analysis so much that new blind spots appear.

## Reuse-First Rule

Prefer reuse of existing written relationship results over repeated analysis.

- if `00_index.md` routes to the right shard, do not scan the whole relationship-map tree
- if a shard summary answers the routing question, do not open multiple shard bodies
- if a curated shard already captures the needed relationship, do not re-derive it from generated artifacts
- if `generated/00_manifest.md` points to the needed evidence, do not scan the whole `generated/` folder
- if an existing maintenance report already identified the stale or conflicting item, do not repeat the same detection work unless fresh verification is required

Written artifacts should reduce repeated context spend, not create more of it.

## Read Budget

Keep the default read budget small.

### `skip`

Use `skip` when the change is clearly mechanical or relationship-neutral.

Default reads:

- none beyond the code you are already changing

Do not open relationship-map docs in this mode unless new evidence suggests the change is not actually relationship-neutral.

### `light`

Use `light` for the middle ground: some relationship impact may exist, but the task does not clearly justify the full workflow.

Default reads:

1. `00_index.md`
2. the `Summary` section of the minimum relevant shard

Optional expansion in `light`:

- the body of one shard only if its summary is insufficient

Do not read by default in `light`:

- `01_usage_and_policy.md`
- `02_audit_log.md`
- `generated/00_manifest.md`
- generated artifacts
- maintenance reports

### `full`

Use `full` only when the change is high-risk, multi-surface, structurally important, or when `light` cannot safely resolve the impact.

Default reads:

1. `00_index.md`
2. relevant shard summaries
3. the body of the relevant curated shard or shards
4. `generated/00_manifest.md` only if curated shards are insufficient

Conditional reads in `full`:

- specific generated artifacts only when needed
- `01_usage_and_policy.md` only for initialization, taxonomy, or policy questions
- `02_audit_log.md` only when history, lifecycle, or approval traceability matters
- maintenance reports only when maintenance findings are directly relevant

## Mode Selection

Use the lightest mode that is still safe.

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

### Lightweight Assessment For `light`

If neither hard gate applies, use only the following low-cost checks:

- does this change alter an existing relationship description
- does it add a reusable relationship edge
- does it make any current shard stale or partial
- is it touching a historically omission-prone chain

Use `skip` if all answers are no.
Use `light` if one answer is yes and the impact remains local.
Upgrade to `full` if multiple answers are yes or if the answer remains unclear after reading `00_index.md` and one shard summary.

## Project Structure

The standard project-scoped relationship-map set is:

- `docs/<project-scope>/relationship-map/00_index.md`
- `docs/<project-scope>/relationship-map/01_usage_and_policy.md`
- `docs/<project-scope>/relationship-map/02_audit_log.md`
- `docs/<project-scope>/relationship-map/critical-chains/`
- `docs/<project-scope>/relationship-map/impact-shards/`
- `docs/<project-scope>/relationship-map/generated/`
- `docs/<project-scope>/relationship-map/generated/00_manifest.md`
- optional: `docs/<project-scope>/relationship-map/maintenance/`
- optional: `docs/<project-scope>/relationship-map/archive/`

Use the templates in `assets/` when creating them.

## Persistent AGENTS Adoption

This skill has two install surfaces:

1. the project-scoped `docs/<project-scope>/relationship-map/` document layer
2. the project-local `AGENTS.md` persistent rule layer

For GitHub-portable setup, treat both as part of initialization.

Use `assets/AGENTS.relationship-map-snippet.template.md` for the persistent rule layer.

Adoption rule:

- if a project-local `AGENTS.md` already exists, append the relationship-map block incrementally
- do not rewrite, replace, or reorganize unrelated `AGENTS.md` content
- if no project-local `AGENTS.md` exists, create one and add the minimum relationship-map block
- keep the `AGENTS.md` block short and durable; detailed workflow stays in `SKILL.md` and the relationship-map docs
- if the repository already has stronger or more specific local rules for relationship-map use, merge carefully instead of creating duplicate contradictory blocks

## Document Roles

- `00_index.md`: routing index, shard registry, freshness overview, and read order
- `01_usage_and_policy.md`: authority boundary, edge taxonomy, freshness policy, and maintenance rules
- `02_audit_log.md`: append-only record of meaningful relationship-map changes
- `critical-chains/`: small human-maintained high-risk end-to-end chains repeatedly hit by bug fixes or feature work
- `impact-shards/`: scoped relationship summaries by capability, module area, or file cluster
- `generated/`: broad machine-generated evidence such as import maps, call maps, or cross-file references
- `generated/00_manifest.md`: routing manifest for generated evidence
- `maintenance/`: maintenance reports and stale or missing map findings
- `archive/`: superseded or archived shards

## Summary-First Rule

Every durable relationship-map artifact should provide a short routing summary at the top.

At minimum:

- `00_index.md` should summarize shard purpose and when to read it
- each curated shard should start with a compact `Summary` block
- maintenance reports should expose key findings near the top
- generated evidence should be discoverable through a compact manifest instead of direct folder scans

The goal is route first, expand second.

## What To Track

Do not limit the map to imports or direct calls.

Track relationship types such as:

- `imports`
- `calls`
- `reads_config`
- `writes_config`
- `invokes_script`
- `produces_artifact`
- `consumes_artifact`
- `validated_by_test`
- `depends_on_contract`
- `entrypoint_for`

For complex experiment or runtime projects, explicitly cover non-code chains such as:

- `python -> shell -> json config -> runtime file -> test/artifact`
- runtime entrypoint -> orchestrator -> adapter -> experiment config -> judge/output path

## Initialization

If relationship maps do not exist yet:

1. Confirm the active project scope.
2. Ask whether to initialize the relationship-map layer for that scope.
3. Create:
   - `docs/<project-scope>/relationship-map/00_index.md`
   - `docs/<project-scope>/relationship-map/01_usage_and_policy.md`
   - `docs/<project-scope>/relationship-map/02_audit_log.md`
   - `docs/<project-scope>/relationship-map/critical-chains/`
   - `docs/<project-scope>/relationship-map/impact-shards/`
   - `docs/<project-scope>/relationship-map/generated/`
   - `docs/<project-scope>/relationship-map/generated/00_manifest.md`
   - optional `maintenance/` and `archive/`
4. Add the persistent relationship-map rule block to the project-local `AGENTS.md`:
   - append `assets/AGENTS.relationship-map-snippet.template.md` if `AGENTS.md` already exists
   - create `AGENTS.md` first only when the project does not already have one
   - do not replace unrelated existing `AGENTS.md` content
5. Start with a minimal useful scope, not a whole-repo giant map.
6. Prefer one or two high-risk chains first.

## Sharding Strategy

Do not shard by only one axis.

Use a practical mix:

- by capability or workflow when failures are cross-directory
- by module or directory when ownership is stable
- by chain when a bug repeatedly spans runtime, config, script, and test surfaces

Good shards are:

- small enough to read quickly
- large enough to cover one meaningful change surface
- stable enough to stay useful across multiple edits

## Use Workflow

Before a non-trivial bug fix or feature change:

1. choose `skip`, `light`, or `full`
2. if the mode is `skip`, do not open relationship-map docs
3. if the mode is `light` or `full`, route through `00_index.md`
4. read only the minimum relationship-map docs allowed for that mode
5. if needed, produce an explicit change-impact checklist:
   - likely files to edit
   - upstream or downstream files to inspect
   - configs or scripts that may need updates
   - tests or validation artifacts that must be rechecked
6. only then start editing

Do not rely on memory alone for multi-file change impact when a written map exists.

## Update Workflow

After a meaningful change:

1. re-check whether the edited files touched any curated chain or shard
2. if relationship meaning did not change, prefer freshness-only or no map update
3. if stable relationship meaning changed, update only the affected shard or shards
4. keep `00_index.md` synchronized when shard status, freshness, or routing changed
5. append to `02_audit_log.md` only when the change is materially traceable
6. tell the user explicitly if the update is structural

Treat shard update plus index update as one documentation action.

## Maintain Workflow

Use maintenance for periodic upkeep, not as the default path for ordinary tasks.

Maintenance should usually:

1. refresh generated evidence
2. refresh `generated/00_manifest.md`
3. compare generated evidence against curated shards only where needed
4. flag stale, missing, conflicting, or deletion-review candidates
5. write a maintenance report only when there are material findings or a scheduled run requires one
6. append a factual audit entry only when the run materially refreshed evidence or changed artifact state

Keep maintenance conservative.
Structural or semantic decisions should be surfaced to the user rather than silently applied.

## Review Loop

Use relationship maps to drive review, not to replace review.

Require a review pass when any of the following is true:

- `>= 3` files changed
- the change crosses `>= 2` surfaces among code, config, script, tests, artifacts, or relationship-map docs
- an entrypoint, shared contract, or core config format changed
- the change-impact checklist contains `>= 5` follow-up checks
- an existing `critical-chain` was touched

After a non-trivial change or when one of the above thresholds is met, review from at least these angles:

- changed file correctness
- upstream or downstream impact coverage
- config and script coverage
- validation coverage
- stale relationship-map entries created by the change

Relationship-map-driven review is only one review input.
Also inspect the actual diff, search the surrounding code, and verify behavior with the appropriate tests or runtime checks.

## Rare Path References

Open these only when the task actually needs them:

- `references/conflict-lifecycle-and-deletion.md`
  - shard conflict handling
  - status selection
  - lifecycle transitions
  - deletion-candidate rules
- `references/audit-and-automation.md`
  - audit minimum set
  - periodic maintenance detail
  - automation guardrails
  - maintenance reporting expectations
- `references/automation-workflow.md`
  - recurring maintenance design

## Templates

Use:

- `assets/AGENTS.relationship-map-snippet.template.md`
- `assets/00_index.template.md`
- `assets/01_usage_and_policy.template.md`
- `assets/02_audit_log.template.md`
- `assets/critical-chain.template.md`
- `assets/impact-shard.template.md`
- `assets/generated-manifest.template.md`
- `assets/maintenance-report.template.md`
- `assets/automation-prompt.template.md`

## Practical Default

When the user wants a first useful version:

- add the minimal relationship-map block to project-local `AGENTS.md` incrementally, or create `AGENTS.md` only if missing
- initialize one project-scoped relationship-map layer
- create `00_index.md` and `01_usage_and_policy.md`
- create `02_audit_log.md`
- create one or two `critical-chains/` shards for the highest-risk workflows
- create only a few `impact-shards/` for the active change surface
- add automation later, after the manual workflow is demonstrably useful
