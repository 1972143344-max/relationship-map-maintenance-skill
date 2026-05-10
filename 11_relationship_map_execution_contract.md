# Relationship-Map Execution Contract

Use this contract when the round enters relationship-map updates, audit, maintenance, structural change, or review-threshold handling.

## Read This When

Read this document before acting when the round involves:

- updating curated shards or `00_index.md`
- changing freshness, status, archive, or supersede state
- appending `02_audit_log.md`
- writing a maintenance report
- handling conflict, lifecycle, deletion review, or approved deletion
- judging whether the round needs relationship-map-driven review escalation

## Skip This When

You may skip this document for:

- pure chat
- read-only routing with no relationship-map modification or sync decision
- clearly `skip`-eligible code changes that do not touch relationship-map artifacts

## Update Triggers

### Freshness-Only Update

Use a freshness-only update when:

- relationship meaning did not change
- the shard only needs a freshness, confidence, or verification refresh

Keep the update narrow.

### Relationship-Meaning Update

Update the affected curated shard when:

- stable relationship meaning changed
- a reusable relationship edge was added or removed
- a change-impact checklist materially changed

### Structural Update

Treat the round as structural when it changes future reading behavior through:

- archive
- supersede
- merge
- split
- deletion-candidate transition
- approved physical deletion

Structural changes require explicit user notice.

## Same-Round Sync Rule

Treat shard update plus index update as one documentation action when shard status, freshness, routing, or relationship meaning changed materially.

Update `00_index.md` in the same round when:

- a curated shard was added
- a shard changed status
- a shard changed freshness in a way that affects routing trust
- a canonical successor or archive path changed

## Audit Minimum Set

Always append an audit entry for:

- initialization of a new relationship-map layer
- creation of a new curated shard
- lifecycle transitions
- structural changes
- maintenance runs that materially refreshed evidence or changed artifact state
- approved deletion

An audit entry is optional for:

- tiny wording cleanups with no meaning change
- mechanical formatting updates
- no-op maintenance runs with no material findings

## Maintenance Reporting

Write a maintenance report only when:

- there are material findings, or
- a scheduled run requires one

Keep reports factual and separated:

- `Findings`
- `Suggested Actions`
- `Needs User Confirmation`

Do not blur confirmed observations and recommendations into one section.

## Structural Notify Rule

Do not silently change what future agents will read first.

Tell the user explicitly before or while performing:

- archive or supersede actions
- shard merge or split
- deletion-candidate promotion
- approved physical deletion
- changes that materially reorganize index or maintenance routing

## Deletion Rule

Deletion review is not deletion.

When an artifact reaches `deletion-candidate`:

1. record the transition in `02_audit_log.md`
2. include it in a maintenance report when appropriate
3. tell the user what is proposed for deletion and why
4. delete only after explicit user approval

If deletion is approved, record:

- deleted path
- prior status
- reason
- approval source
- deletion timestamp

## Review Thresholds

Require a review pass when any of these is true:

- `>= 3` files changed
- the change crosses `>= 2` surfaces among code, config, script, tests, artifacts, or relationship-map docs
- an entrypoint, shared contract, or core config format changed
- the change-impact checklist contains `>= 5` follow-up checks
- an existing `critical-chain` was touched

Relationship-map-driven review must not substitute for direct diff inspection, targeted search, tests, runtime validation, or independent review when those are required.

## Closure Rule

Do not treat relationship-map updates alone as proof that the underlying engineering work is complete.

Relationship-map closure is ready only when:

- the relationship artifacts were updated truthfully
- required index or audit sync has happened
- required review escalation has happened, if triggered
- remaining uncertainty or partial coverage is surfaced honestly
