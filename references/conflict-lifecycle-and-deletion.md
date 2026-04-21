# Conflict, Lifecycle, And Deletion

Use this file only when shard conflict, lifecycle transition, archival, supersede handling, or deletion review is part of the task.

## Conflict Handling

Handle conflicts explicitly instead of letting incompatible current-state shards accumulate.

- if current code conflicts with a curated shard, treat the code as implementation reality and mark the shard `partial` or `stale` until re-verified
- if governance docs conflict with a relationship shard on intended behavior, governance wins and the shard must be updated or downgraded
- if a curated shard conflicts with generated evidence, do not overwrite it blindly; inspect the code or produce a maintenance finding
- if two curated shards describe incompatible current-state relationships, do not leave both as active without clarification; supersede, split, downgrade, or archive one of them
- if `00_index.md` and shard state disagree, update them in the same round

## Conflict Confidence Levels

Do not stop work automatically just because a conflict exists.
Choose the narrowest safe handling based on confidence.

### High Confidence

Use this when current code, governance, or strong evidence clearly supports one shard over the other.

- keep the better-supported shard active
- downgrade the weaker shard to `stale` or `superseded`
- update the index in the same round
- append an audit entry
- tell the user what was changed

### Medium Confidence

Use this when one direction is more likely correct, but the replacement is not fully proven.

- do not keep both shards as active current-state truth
- keep the more likely shard usable if needed
- downgrade the weaker shard to `partial` or `stale`
- avoid `superseded` unless replacement is reasonably clear
- record the uncertainty in the shard or audit trail
- continue the task if the remaining uncertainty does not change implementation direction
- report the tentative choice to the user in the same turn

### Low Confidence

Use this when the agent cannot safely determine which shard is correct and the evidence is too weak for a tentative current-state choice.

- do not leave both shards as active
- downgrade at least one shard, and downgrade both if needed
- record the conflict in maintenance or audit artifacts
- continue with work that does not depend on the unresolved conflict
- ask the user only if the unresolved conflict would change implementation direction, deletion, or authoritative conclusions

## Status Selection Rule

Use statuses intentionally:

- `superseded` when the replacing shard is sufficiently clear
- `stale` when the shard can no longer be trusted as current, but the replacement is not confirmed
- `partial` when a tentative direction exists but verification is incomplete

Prefer temporary downgrade plus explicit reporting over false certainty.

## Lifecycle

Default lifecycle:

`active -> partial -> stale -> superseded -> archived -> deletion-candidate`

Use the earliest state that honestly reflects the artifact's condition.

- `active`: current and usable
- `partial`: partly re-verified but incomplete
- `stale`: not safe to trust without re-checking
- `superseded`: replaced by a newer shard
- `archived`: historical and not part of the default read path
- `deletion-candidate`: old enough and low-value enough to consider physical deletion, but still awaiting user approval

Do not jump straight to deletion for normal maintenance.
Prefer state transition first, then user review.

## Deletion Review

When something reaches `deletion-candidate`:

1. record the transition in `02_audit_log.md`
2. include it in a maintenance report
3. tell the user what is proposed for deletion and why
4. delete only after explicit user approval

If deletion is approved, record:

- deleted path
- prior status
- reason
- approval source
- deletion timestamp

## Deletion-Candidate Entry Criteria

Do not mark something as `deletion-candidate` just because it is old.

Prefer this status only when all or nearly all of the following are true:

- the artifact is already `archived` or clearly no longer part of the active read path
- it has a known replacement, or repeated maintenance has found no current use for it
- it is not listed as an active current-state shard in `00_index.md`
- it has not been materially updated or relied on recently
- deleting it would not remove the only readable record of an important chain or decision

If these conditions are only partly met, prefer `archived` or `stale` over `deletion-candidate`.
