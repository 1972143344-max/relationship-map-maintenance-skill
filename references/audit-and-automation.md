# Audit And Automation

Use this file only when audit traceability, periodic maintenance detail, or automation behavior is part of the task.

## Audit Minimum Set

`02_audit_log.md` should not try to log everything.
It should reliably capture the minimum set of events that matter for traceability.

Always append an audit entry for:

- initialization of a new relationship-map layer
- creation of a new curated shard
- lifecycle transitions such as `active -> stale`, `stale -> superseded`, `archived -> deletion-candidate`
- structural changes such as merge, split, archive, supersede, or restore
- periodic maintenance runs that materially refreshed generated evidence or changed shard states
- approved physical deletion

An audit entry is optional for:

- tiny wording cleanups that do not change meaning
- mechanical formatting changes
- no-op maintenance runs with no material findings

## Periodic Maintenance Detail

Periodic maintenance is for keeping the map useful, not for silently rewriting project knowledge.

Default periodic maintenance should:

1. scan the configured scope
2. refresh machine-generated evidence in `generated/`
3. refresh `generated/00_manifest.md`
4. compare current evidence against curated shards
5. flag stale shards, missing high-risk chains, or inconsistent edge descriptions
6. detect reasonable `deletion-candidate` artifacts
7. write a maintenance report under `maintenance/` only when there are material findings or a scheduled run requires one
8. append a factual audit entry if the maintenance run materially refreshed generated evidence or changed artifact states
9. propose follow-up updates instead of silently making structural shard decisions

When flagging `deletion-candidate` artifacts, explain which entry criteria were satisfied and which, if any, remain uncertain.

Periodic maintenance is always `full` mode, but it should still follow progressive disclosure:

- use `generated/00_manifest.md` instead of scanning generated artifacts blindly
- use `00_index.md` before opening curated shards
- only open the shards directly implicated by the maintenance findings

## Automation Guardrails

Automation is allowed, but keep it conservative.

Automation may:

- refresh generated evidence
- update mechanical timestamps or freshness markers when clearly justified
- produce maintenance reports
- flag suspected missing or stale shards
- flag deletion candidates
- append factual audit entries for maintenance runs or status transitions

Automation must not silently:

- rewrite curated shard meaning
- archive or supersede shards
- merge or split shard structure
- promote stable findings into governance docs
- physically delete artifacts
- claim a relationship is confirmed without evidence

If an automation proposes a structural or semantic update, surface it to the user or leave it as a report item for interactive review.

## Maintenance Reporting Expectation

Maintenance reports should stay concise and operational.

At minimum, report:

- scope checked
- evidence refreshed
- shards flagged as stale, partial, conflicting, or missing
- artifacts proposed for deletion review
- follow-up actions that still require interactive confirmation

Use this structure by default:

- `Findings`: factual observations only
- `Suggested Actions`: recommended next steps, clearly separated from facts
- `Needs User Confirmation`: structural, semantic, or destructive actions that must not be applied silently

Do not blur findings and recommendations into one section.

## Post-Report And Post-Change Check

Distinguish report generation from actual modification.

- if automation only refreshes generated evidence, writes a report, or appends a factual audit entry, perform a brief sanity check on the report and changed factual outputs
- if a later interactive step performs real relationship-map modifications, use the normal review thresholds instead of treating the report-only pass as sufficient

The sanity check should confirm at least:

- the report did not invert or overstate the evidence
- flagged items are routed to the correct shard or artifact
- suggested actions are separated from confirmed facts
- explicit user-confirmation items are still clearly marked

Escalate to a full review pass after modification when any of these is true:

- `>= 3` files changed
- the change crosses `>= 2` surfaces among code, config, script, tests, artifacts, or relationship-map docs
- an entrypoint, shared contract, or core config format changed
- the change-impact checklist contains `>= 5` follow-up checks
- an existing `critical-chain` was touched
