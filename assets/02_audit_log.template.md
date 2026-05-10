# Maintenance Threshold

- Thresholds:
  - checkpoint or split this audit log when it grows past `220` lines or when a new reader can no longer quickly locate the latest materially relevant change
  - if one log starts mixing too many unrelated maintenance eras, prefer checkpoint summaries or archive slicing
- Trigger:
  - if this audit log is over threshold or difficult to route, explicitly tell the user that audit-log maintenance is needed and propose checkpointing or archival slicing rather than endless append-only growth

# Summary

- Purpose: append-only audit log for relationship-map changes, maintenance runs, lifecycle transitions, and approved deletions
- Authority: factual history only; does not redefine current shard truth
- Update when: curated shards, lifecycle states, generated refreshes, or approved deletions change the relationship-map layer materially
- Read this when: history, traceability, lifecycle transitions, or deletion approval matters
- Skip this when: the current task only needs ordinary routing or one current shard and no history-sensitive judgment is being made

Always log:

- initialization
- curated shard creation
- lifecycle transitions
- structural changes
- material maintenance runs
- approved deletion

# Relationship Map Audit Log

## Entry Template

- timestamp:
- actor:
- action_type:
- scope:
- affected_artifacts:
- summary:
- result:
- follow_up:

## Entries

- timestamp:
  actor:
  action_type:
  scope:
  affected_artifacts:
  summary:
  result:
  follow_up:
