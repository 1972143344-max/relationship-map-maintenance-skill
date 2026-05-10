# Relationship-Map Surface Catalog

Use this sidecar when you need the full document set, stable entrypoints, or template routing for the relationship-map layer.

## Standard Relationship-Map Set

Default project-scoped relationship-map files:

- `docs/<project-scope>/relationship-map/00_index.md`
- `docs/<project-scope>/relationship-map/01_usage_and_policy.md`
- `docs/<project-scope>/relationship-map/02_audit_log.md`
- `docs/<project-scope>/relationship-map/critical-chains/`
- `docs/<project-scope>/relationship-map/impact-shards/`
- `docs/<project-scope>/relationship-map/generated/`
- `docs/<project-scope>/relationship-map/generated/00_manifest.md`
- optional: `docs/<project-scope>/relationship-map/maintenance/`
- optional: `docs/<project-scope>/relationship-map/archive/`

## Support Protocol Surfaces

- `10_relationship_map_runtime_protocol.md`
- `11_relationship_map_execution_contract.md`

Treat these as stable support-entrypoint surfaces when the runtime router or documentation points the current action into them.

## Stable Entrypoints And Default Split Rule

Treat these as stable read-first entrypoints by default:

- `00_index.md`
- `10_relationship_map_runtime_protocol.md`
- `11_relationship_map_execution_contract.md`

If one of those entrypoints grows too large, keep the entrypoint as the shallow read-first surface and split below it with second-level routing by semantic topic, layer, or active-versus-historical boundary rather than renaming the entrypoint itself.

## Document Roles

- `00_index.md`: routing index, shard registry, freshness overview, and read order
- `01_usage_and_policy.md`: authority boundary, edge taxonomy, freshness policy, and maintenance rules
- `02_audit_log.md`: append-only record of meaningful relationship-map changes
- `critical-chains/`: small human-maintained end-to-end chains repeatedly hit by bug fixes or feature work
- `impact-shards/`: scoped relationship summaries by capability, module area, or file cluster
- `generated/`: broad machine-generated evidence such as import maps, call maps, or cross-file references
- `generated/00_manifest.md`: routing manifest for generated evidence
- `maintenance/`: maintenance reports and stale or missing map findings
- `archive/`: superseded or archived shards

## Asset Routing

When creating repo-local relationship-map docs, reuse bundled templates under `assets/`:

- `AGENTS.relationship-map-snippet.template.md`
- `00_index.template.md`
- `01_usage_and_policy.template.md`
- `02_audit_log.template.md`
- `critical-chain.template.md`
- `impact-shard.template.md`
- `generated-manifest.template.md`
- `maintenance-report.template.md`
- `automation-prompt.template.md`
