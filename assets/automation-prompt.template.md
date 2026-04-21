Refresh generated relationship evidence for the active project scope, update `generated/00_manifest.md`, compare the evidence against curated `critical-chains/` and `impact-shards/`, and write a maintenance report under `docs/<project-scope>/relationship-map/maintenance/`.

Rules:

- do not silently rewrite curated shard semantics
- do not archive, supersede, merge, or split curated shards
- do not physically delete artifacts
- flag stale or likely missing shards instead of silently fixing structure
- flag deletion candidates instead of deleting them
- append a factual audit entry if generated evidence or lifecycle state changed materially
- keep the report compact and action-oriented
- structure the report as `Findings`, `Suggested Actions`, and `Needs User Confirmation`
- keep recommendations separate from confirmed observations
- if evidence is insufficient, say so explicitly
- after producing the report, do a brief sanity check on the report and factual outputs
- if a later step applies real relationship-map modifications, use the normal review thresholds instead of treating report generation as the final review
