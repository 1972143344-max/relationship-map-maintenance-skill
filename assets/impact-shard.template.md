# Maintenance Threshold

- Thresholds:
  - split or refactor this shard when it grows past `160` lines, `12` primary nodes, or `14` important relationships
  - if one shard starts mixing multiple unrelated change surfaces, treat it as semantically oversized even before the line threshold
- Trigger:
  - if this shard is over threshold or semantically oversized, explicitly tell the user that shard refactoring is needed and propose a semantic split rather than adding more unrelated edges into one file

# Summary

- Type: impact shard
- Purpose: scoped relationship summary for one capability, module cluster, or change surface
- Authority: routing and impact aid only; if current code or authoritative governance docs conflict with this shard, code and governance win and the shard should be refreshed in the same workstream
- Read this when: a task touches this area and needs upstream/downstream impact analysis
- Skip this when: the routing question is already answered by `00_index.md` or the current round is clearly outside this shard's change surface

# Metadata

- id:
- scope:
- status: active
- last_verified_at:
- freshness: fresh
- confidence: medium
- supersedes:
- superseded_by:

# Primary Nodes

- file or module:
- why included:

# Important Relationships

| from | edge_type | to | confidence | notes |
| --- | --- | --- | --- | --- |
| | | | | |

# Change-Impact Checklist

- if this area changes, inspect:
- if runtime behavior changes, inspect:
- if config changes, inspect:
- if output format changes, inspect:
- tests or artifacts to re-check:

# Known Gaps

- 

# Evidence Sources

- human:
- generated:
