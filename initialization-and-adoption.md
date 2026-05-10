# Initialization And Adoption

Use this sidecar only when the current action is first-time setup or adoption of an existing project into the relationship-map layer.

## Initialization

Use initialization when `docs/<project-scope>/relationship-map/` does not yet exist for the active project scope.

### Initialization Steps

1. Confirm the active project scope.
2. Ask whether to initialize the relationship-map layer for that scope.
3. Create the minimum relationship-map set:
   - `00_index.md`
   - `01_usage_and_policy.md`
   - `02_audit_log.md`
   - `critical-chains/`
   - `impact-shards/`
   - `generated/`
   - `generated/00_manifest.md`
4. Add the persistent relationship-map rule block to the project-local `AGENTS.md`:
   - append it if `AGENTS.md` already exists
   - create `AGENTS.md` only when missing
   - do not rewrite unrelated `AGENTS.md` content
5. Start with one or two high-risk chains, not a whole-repo giant map.
6. Add maintenance or archive surfaces only when a real workflow justifies them.

### Initialization Outcome

Initialization should make these explicit:

- active project scope
- relationship-map root
- whether `maintenance/` exists yet
- whether `archive/` exists yet
- whether a project-local `AGENTS.md` block was appended or newly created

## Adoption

Use adoption when the repo already has scattered relationship docs, stale impact notes, generated evidence, or historical shards.

### Adoption Steps

1. Confirm the active project scope and current relationship-map root.
2. Read only the minimum existing material needed to classify it.
3. Classify existing artifacts as:
   - active curated routing
   - generated evidence
   - maintenance/reporting
   - archived or historical
4. Create or refresh `00_index.md` so future routing is explicit.
5. Merge the minimal relationship-map block into project-local `AGENTS.md` without rewriting unrelated rules.
6. Do not mass-clean old material unless the user asks.

### Adoption Rule

Adoption should classify first and reorganize second.

Do not silently treat old notes, generated artifacts, or stale shards as active curated truth merely because they are detailed.
