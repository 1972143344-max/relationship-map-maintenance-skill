# Summary

- Purpose: route relationship-map reads to the minimum relevant curated shard before falling back to generated evidence
- Authority: routing-only; source files and governance docs remain higher authority
- Read this first when: a task needs change-impact analysis, chain tracing, or relationship-map maintenance

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
