Refresh generated relationship evidence for the active project scope, update `generated/00_manifest.md`, compare the evidence against curated `critical-chains/` and `impact-shards/`, and write a maintenance report under `docs/<project-scope>/relationship-map/maintenance/`.

Rules:

- do not silently rewrite curated shard semantics
- do not archive, supersede, merge, or split curated shards
- do not physically delete artifacts
- flag stale or likely missing shards instead of silently fixing structure
- flag deletion candidates instead of deleting them
- append a factual audit entry if generated evidence or lifecycle state changed materially
- keep the report compact and action-oriented
- if evidence is insufficient, say so explicitly
