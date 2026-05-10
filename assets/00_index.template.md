# Maintenance Threshold

- Thresholds:
  - add a second-level routing split when this index grows past `220` lines or `18` active rows across critical chains, impact shards, maintenance queue, and deletion candidates
  - if the index can no longer route most tasks to one next shard or one next document hop, treat it as noisy even before the line threshold
- Trigger:
  - if this index is over threshold or has become noisy to route, explicitly tell the user that relationship-map routing maintenance is needed and propose a second-level routing split rather than letting repeated scans grow silently

# Summary

- Purpose: route relationship-map reads to the minimum relevant curated shard before falling back to generated evidence
- Authority: routing-only support; current code and authoritative governance docs remain higher authority, and detected drift should be fixed in the same workstream
- Read this first when: a task needs change-impact analysis, chain tracing, or relationship-map maintenance
- Skip this when: the round is clearly `skip` and relationship impact is already known to be neutral

# Relationship Map Index

## Scope

- Project scope:
- Root path:
- Last reviewed:

## Read Order

1. This index
2. Relevant `critical-chains/` shard
3. Relevant `impact-shards/` shard
4. `generated/` evidence only if curated shards are missing, stale, or insufficient
5. `02_audit_log.md` only when history, maintenance actions, or lifecycle transitions matter

## Critical Chains

| id | title | status | freshness | confidence | summary | when to read | canonical_successor | archive_path |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| | | | | | | | | |

## Impact Shards

| id | title | scope | status | freshness | confidence | summary | when to read | canonical_successor | archive_path |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| | | | | | | | | | |

## Generated Evidence

Read `generated/00_manifest.md` first. Do not scan the full `generated/` folder by default.

| manifest_status | last_refreshed | notes |
| --- | --- | --- |
| | | |

## Maintenance Queue

| item | severity | affected shard | action needed | notes |
| --- | --- | --- | --- | --- |
| | | | | |

## Deletion Candidates

| artifact | current_status | why candidate | user approval needed |
| --- | --- | --- | --- |
| | | | |
