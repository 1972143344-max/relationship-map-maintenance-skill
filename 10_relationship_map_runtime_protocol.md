# Relationship-Map Runtime Protocol

Use this protocol when non-trivial repo work depends on relationship-map routing, read-budget control, or curated-vs-generated expansion quality.

## Read This When

Read this document before acting when the round involves:

- deciding `skip`, `light`, or `full`
- routing through `00_index.md`, curated shards, `generated/00_manifest.md`, or generated artifacts
- choosing how far to expand relationship-map reading
- deciding whether a summary is enough or whether a shard body is needed

## Skip This When

You may skip this document for:

- pure chat
- light brainstorming with no repo-document lookup
- clearly local, relationship-neutral changes that already satisfy the `skip` gate

## Core Order

Use this focused routing order:

1. mode gate first
2. curated routing second
3. generated evidence third
4. policy, audit, and maintenance detail only on demand

## Mode Defaults

### `skip`

Read:

- no relationship-map docs by default

Do not read:

- `00_index.md`
- curated shards
- `generated/00_manifest.md`
- generated artifacts
- maintenance reports

Upgrade out of `skip` only if new evidence suggests the change is not actually relationship-neutral.

### `light`

Read:

1. `00_index.md`
2. the `Summary` section of the minimum relevant shard

Optional expansion:

- the body of one shard only if its summary is insufficient

Do not read by default:

- `01_usage_and_policy.md`
- `02_audit_log.md`
- `generated/00_manifest.md`
- generated artifacts
- maintenance reports

### `full`

Read:

1. `00_index.md`
2. relevant shard summaries
3. the body of the relevant curated shard or shards
4. `generated/00_manifest.md` only if curated shards are insufficient

Conditional reads:

- specific generated artifacts only when the manifest indicates they are needed
- `01_usage_and_policy.md` only for taxonomy, policy, or initialization questions
- `02_audit_log.md` only when history, lifecycle, or approval traceability matters
- maintenance reports only when maintenance findings are directly relevant

## Runtime Document Classes

After routing begins, treat each document type differently.

- `00_index.md`
  - read first for curated routing
  - use it to narrow to the minimum relevant shard
- curated shard summary
  - use to decide whether the shard body is needed
- curated shard body
  - read only when the summary is insufficient for safe impact analysis
- `generated/00_manifest.md`
  - read before any generated artifact
  - use it to avoid scanning the whole `generated/` folder
- generated artifact
  - read only when curated material is missing, stale, conflicting, or insufficient
- `01_usage_and_policy.md`
  - read only for policy, taxonomy, initialization, or conflict-rule questions
- `02_audit_log.md`
  - read only when history, lifecycle, or deletion approval traceability matters
- maintenance report
  - read only when maintenance findings are directly relevant to the current action

## Reuse-First Reading

Prefer the minimum useful written artifact:

- index before tree scan
- shard summary before shard body
- curated shard before generated evidence
- generated manifest before generated folder scan
- prior maintenance report before re-running the same stale-detection reasoning

## Governing Expansion

Expand beyond the first routed artifact only when the current layer cannot safely answer:

- which files or surfaces need inspection
- whether shard freshness or relationship meaning changed
- whether generated evidence is actually needed

If you cannot state which one of those questions requires the next read, stop expanding and reassess.

## Stop Rule

Stop expanding when all three are true:

1. the minimum relevant relationship surface is identified
2. the current impact or update decision is safe to make
3. more reading would not materially change the next inspection, update, or escalation step

## Truth Boundary

Repeat this rule wherever routing and maintenance meet:

- relationship maps are maintained routing and impact support
- code and authoritative governance remain higher authority
- if they conflict, refresh the affected map instead of forcing the code to match the map
