# Summary

- Purpose: append-only audit log for relationship-map changes, maintenance runs, lifecycle transitions, and approved deletions
- Authority: factual history only; does not redefine current shard truth
- Update when: curated shards, lifecycle states, generated refreshes, or approved deletions change the relationship-map layer materially

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
