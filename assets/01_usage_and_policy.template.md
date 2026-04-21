# Summary

- Purpose: define how relationship-map artifacts are written, read, and maintained
- Authority: policy for the relationship-map layer only; does not override governance docs
- Read this when: initializing or maintaining the relationship-map layer for this project scope

# Usage And Policy

## Authority Boundary

- Source code, runtime files, configs, scripts, tests, and artifacts are the implementation ground truth.
- Governance docs remain authoritative for intended behavior, constraints, and decisions.
- Curated relationship-map shards are compact working maps for impact analysis.
- Generated evidence is broad coverage input, not automatically trusted curated knowledge.

## Progressive Disclosure

- Read `00_index.md` first for routing.
- Read only the minimum relevant curated shard summary before expanding into full shard content.
- Read `generated/00_manifest.md` before opening any generated artifact.
- Read `02_audit_log.md` only when history, transitions, or deletion approval matters.
- Do not scan entire folders by default when a summary or manifest can route you first.

## Maintenance Modes

- `skip`: no relationship-map reads for clearly mechanical or relationship-neutral changes
- `light`: read `00_index.md` and the minimum relevant shard summary only; avoid policy, audit, generated, and maintenance docs by default
- `full`: read `00_index.md`, relevant shard summaries and bodies, then `generated/00_manifest.md` only if curated shards are insufficient

Do not default to `full` just because the skill triggered.

## Trigger Gates

Use `skip` directly when the change is clearly mechanical, local, relationship-neutral, and touches no shared contract, entrypoint, core config format, or existing `critical-chain`.

Use `full` directly when any of these is true:

- `>= 3` files changed
- `>= 2` surfaces changed among code, config, script, tests, artifacts, or relationship-map docs
- entrypoint, shared contract, or core config format changed
- a `critical-chain` was touched
- the expected change-impact checklist would contain `>= 5` follow-up checks
- shard conflict, structural change, deletion review, or maintenance automation is involved

If neither gate applies, use a lightweight assessment based on `00_index.md` and one shard summary.

## Edge Types

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

Add new edge types only when they repeatedly improve change-impact accuracy.

## Freshness Labels

- `fresh`: recently checked against current code or generated evidence
- `partial`: some edges were re-checked but coverage is incomplete
- `stale`: do not trust without re-checking

## Confidence Labels

- `high`: human-confirmed from code or repeated observed behavior
- `medium`: mixed human plus generated evidence
- `low`: preliminary or generated-only

## Maintenance Rules

- Update `00_index.md` whenever curated shard status or freshness changes materially.
- Treat shard update plus index update as one documentation action.
- Do not silently archive, supersede, merge, or split curated shards that change future reading behavior.
- Prefer adding missing follow-up checks over adding more descriptive prose.
- Promote repeatedly important end-to-end chains into `critical-chains/`.
- Record meaningful relationship-map changes in `02_audit_log.md`.

## Conflict Handling

- If code conflicts with a curated shard, code is the current implementation reality and the shard should be downgraded or refreshed.
- If governance conflicts with a relationship shard on intended behavior, governance wins.
- If two curated shards conflict, do not leave both as active current-state truth without clarification.
- If index state and shard state disagree, update them in the same round.

### Conflict Confidence Levels

- High confidence: keep the better-supported shard active, downgrade the weaker shard to `stale` or `superseded`, update the index, and log the action.
- Medium confidence: keep a tentative direction only if needed, downgrade the weaker shard to `partial` or `stale`, avoid `superseded` unless replacement is clear, and report the uncertainty.
- Low confidence: do not leave both shards active, downgrade one or both, record the conflict, continue unaffected work, and ask the user only if the conflict changes implementation direction or authoritative conclusions.

### Status Selection Rule

- `superseded` when replacement is sufficiently clear
- `stale` when the shard is no longer trusted as current but no confirmed replacement exists
- `partial` when a tentative direction exists but verification is incomplete

## Lifecycle

- `active`
- `partial`
- `stale`
- `superseded`
- `archived`
- `deletion-candidate`

Use physical deletion only after explicit user approval.

### Deletion-Candidate Entry Criteria

Prefer `deletion-candidate` only when the artifact is already outside the active read path, has a known replacement or no observed current use, is not still listed as active in the index, and deleting it would not remove the only readable record of an important chain.

## Review Thresholds

Require a review pass when any of these is true:

- `>= 3` files changed
- `>= 2` surfaces changed among code, config, script, tests, artifacts, or relationship-map docs
- entrypoint, shared contract, or core config format changed
- change-impact checklist has `>= 5` follow-up checks
- a `critical-chain` was touched

## Automation Guardrails

- Automation may refresh `generated/` and produce maintenance reports.
- Automation may flag stale shards or likely missing chains.
- Automation may flag deletion candidates and append factual audit entries.
- Automation must not silently rewrite curated shard meaning or structure.
- Automation must not physically delete artifacts without explicit user approval.

## Audit Minimum Set

Always log:

- initialization
- new curated shard creation
- lifecycle transitions
- structural changes
- material maintenance runs
- approved deletion

## Reference-Only Rule

- Relationship maps are a reference layer for better coverage, not a complete substitute for direct code inspection, testing, or review.
- Do not let relationship-map reads replace targeted code search or behavior verification.
