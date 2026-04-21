## Relationship-Map Maintenance

When a project scope has `docs/<project-scope>/relationship-map/`, use it as a reference layer for non-trivial change-impact analysis, post-change updates, and periodic maintenance.

Default path order:

- `use`: pre-change routing and impact analysis
- `update`: post-change freshness or shard updates only when relationship meaning or shard state changed
- `maintain`: periodic or structural upkeep only when actually needed

Do not default to full relationship-map maintenance.
Use the lightest safe mode:

- `skip`: for clearly mechanical or relationship-neutral changes
- `light`: read `00_index.md` and the minimum relevant shard summary only
- `full`: use only when the change is high-risk, multi-surface, structurally important, or when `light` is insufficient

Start with `full` directly when any of the following is true:

- `>= 3` files changed
- the change crosses `>= 2` surfaces among code, config, script, tests, artifacts, or relationship-map docs
- an entrypoint, shared contract, or core config format changed
- an existing `critical-chain` was touched
- the expected change-impact checklist would contain `>= 5` follow-up checks
- conflict handling, deletion review, structural shard change, or relationship-map automation is involved

If none of the above is true, do not expand into the full relationship-map workflow by default.
Use low-cost checks first.
Use `skip` when the change does not alter relationship meaning, add a reusable relationship edge, or change shard freshness or status.
Use `light` only when one of those signals is present but the impact still appears local.

Prefer reuse of existing written relationship-map results over repeated analysis:

- route through `00_index.md` before scanning the tree
- use shard summaries before shard bodies when routing is still uncertain
- use curated shards before generated artifacts when they already answer the relationship question
- use `generated/00_manifest.md` before scanning `generated/`

Do not read these by default during ordinary code changes unless the task actually needs them:

- `docs/<project-scope>/relationship-map/01_usage_and_policy.md`
- `docs/<project-scope>/relationship-map/02_audit_log.md`
- `docs/<project-scope>/relationship-map/generated/00_manifest.md`
- generated artifacts
- maintenance reports

Relationship-map artifacts are reference-only. They do not replace direct code inspection, targeted search, tests, runtime validation, or review.
