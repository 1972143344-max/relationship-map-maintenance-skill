## Relationship-Map Maintenance

Treat this block as a short routing surface, not as a weak summary copy of the whole relationship-map workflow.

When a project scope has `docs/<project-scope>/relationship-map/`, use it as a reference layer for non-trivial change-impact analysis, post-change updates, and periodic maintenance.

Default path order:

- `use`: pre-change routing and impact analysis
- `update`: post-change freshness or shard updates only when relationship meaning or shard state changed
- `maintain`: periodic or structural upkeep only when actually needed

Use the lightest safe mode:

- `skip`: for clearly mechanical or relationship-neutral changes
- `light`: read `00_index.md` and the minimum relevant shard summary only
- `full`: use only when the change is high-risk, multi-surface, structurally important, or when `light` is insufficient

Read `docs/<project-scope>/relationship-map/00_index.md` when:

- the task is non-trivial and relationship impact is plausible
- the round is in `light` or `full`
- you need to choose the minimum relevant curated shard before editing or review

Do not read relationship-map docs by default when:

- the round is clearly `skip`
- the change is local, mechanical, and relationship-neutral
- no shared contract, entrypoint, core config format, or existing `critical-chain` is touched

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
