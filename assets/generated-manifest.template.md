# Maintenance Threshold

- Thresholds:
  - add a second-level generated routing split when this manifest grows past `180` lines or no longer lets most tasks choose one artifact hop quickly
  - if one manifest starts mixing many unrelated generated families, split by artifact family or subsystem
- Trigger:
  - if this manifest is over threshold or noisy to route, explicitly tell the user that generated-evidence routing maintenance is needed and propose a split below the manifest rather than scanning the whole generated folder

# Summary

- Purpose: route agents to the minimum relevant generated evidence without scanning the whole `generated/` folder
- Authority: generated evidence index only; generated artifacts remain evidence, not curated truth, and code plus authoritative governance docs still win on conflict
- Read this when: curated shards are missing, stale, conflicting, or insufficient and you need broader machine-generated coverage
- Skip this when: a curated shard already answers the relationship question

# Generated Evidence Manifest

## Scope

- Project scope:
- Last refreshed:

## Artifacts

| id | artifact | scope | generated_at | source_tool | summary | when to read |
| --- | --- | --- | --- | --- | --- | --- |
| | | | | | | |
