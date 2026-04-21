# Automation Workflow

Use automation conservatively for relationship-map maintenance.

## Recommended Automation Scope

Good recurring automation tasks:

- refresh generated relationship evidence for one active project scope
- refresh `generated/00_manifest.md`
- detect likely stale curated shards
- detect likely missing high-risk chains
- detect likely deletion candidates
- produce a maintenance report for interactive review

Avoid automating semantic shard rewrites by default.

## Default Automation Output

Write a maintenance report under:

- `docs/<project-scope>/relationship-map/maintenance/`

The report should summarize:

- what evidence was refreshed
- whether `generated/00_manifest.md` was refreshed successfully
- which curated shards look stale
- what likely missing chains were detected
- what deletion candidates were detected
- which changes require explicit user review

Use this section order by default:

1. `Findings`
2. `Suggested Actions`
3. `Needs User Confirmation`

Keep recommendations clearly separate from confirmed observations.

## Safe Automation Contract

Automation may:

- refresh generated artifacts
- update mechanical timestamps attached to the generated refresh
- write a maintenance report
- append a factual audit entry for the maintenance run

Automation must not silently:

- rewrite curated shard semantics
- promote, archive, merge, split, or supersede curated shards
- physically delete relationship-map artifacts
- claim confidence above the evidence level

If the automation only produces a report or factual refresh, do a brief sanity check rather than a full review pass.
If a later interactive step applies actual relationship-map changes, run review according to the normal skill thresholds.

## Suggested Recurrence

Use periodic maintenance when one of these is true:

- the project has active frequent edits
- the same chain is being touched repeatedly
- stale relationship maps have already caused missed updates

Keep the first automation narrow:

- one project scope
- one or two chain families
- maintenance report only
