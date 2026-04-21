# Relationship Map Maintenance

`relationship-map-maintenance` is a project-scoped skill for maintaining a compact relationship and change-impact layer around complex code changes.

It is meant for repositories where fixes and features regularly cross file, module, config, script, and test boundaries, and where "updated one place, missed another" is a recurring failure mode.

This skill does not try to replace code reading, testing, or review. It adds a small written layer that makes impact paths easier to route before a change and easier to update after a change.

## What It Adds

- A project-scoped `docs/<project-scope>/relationship-map/` document set
- A minimal `AGENTS.md` block for persistent, low-cost routing rules
- Curated `critical-chains/` and `impact-shards/` for high-value change surfaces
- A generated-evidence manifest so agents do not need to scan large folders by default
- Conservative maintenance rules for conflict handling, lifecycle changes, audit logging, and automation

## Design Goals

- Keep the default path short
- Prefer route-first reading over bulk reading
- Reuse written results before re-deriving relationships
- Make map maintenance cheaper than the omissions it is trying to prevent
- Keep structural or destructive actions explicit

## Default Operating Model

The default path is:

- `use`: route before a non-trivial change
- `update`: refresh only the touched relationship entries after a meaningful change
- `maintain`: run periodic upkeep only when needed

The skill uses three maintenance levels:

- `skip`: no relationship-map reads for clearly local, relationship-neutral changes
- `light`: read `00_index.md` and the minimum relevant shard summary only
- `full`: expand only when the change is high-risk, multi-surface, structurally important, or unresolved by `light`

## Repository Layout

```text
relationship-map-maintenance/
  SKILL.md
  README.md
  README.zh-CN.md
  agents/
    openai.yaml
  assets/
    AGENTS.relationship-map-snippet.template.md
    00_index.template.md
    01_usage_and_policy.template.md
    02_audit_log.template.md
    critical-chain.template.md
    impact-shard.template.md
    generated-manifest.template.md
    maintenance-report.template.md
    automation-prompt.template.md
  references/
    audit-and-automation.md
    automation-workflow.md
    conflict-lifecycle-and-deletion.md
```

## Installation

Copy the skill directory into your Codex skills location.

If the skill is used as a project-local skill, keep it under the repository's local skills directory.
If it is used as a user-level skill, install it under the user's Codex skills directory.

## Initialization

Initialization has two parts.

1. Create the project-scoped relationship-map document layer under `docs/<project-scope>/relationship-map/`.
2. Add the minimal relationship-map rule block to the project-local `AGENTS.md`.

The `AGENTS.md` integration is incremental:

- if `AGENTS.md` already exists, append the relationship-map block
- do not rewrite or reorganize unrelated `AGENTS.md` content
- create `AGENTS.md` only if the project does not already have one

Use `assets/AGENTS.relationship-map-snippet.template.md` for that block.

## When To Use It

Use this skill when:

- a bug fix spans multiple files or surfaces
- a change touches shared contracts, entrypoints, or core config formats
- a project has repeated omissions across call chains or workflow chains
- you want a durable impact layer that can be reused during review and follow-up work

Do not use it as the only basis for implementation or review.
Code, tests, runtime checks, and direct inspection remain necessary.

## Maintenance And Automation

The skill keeps maintenance conservative.

- generated evidence may be refreshed
- stale or conflicting shards may be flagged
- reports may be written when there are material findings or when a scheduled run requires one
- structural shard decisions should not be applied silently
- physical deletion requires explicit user approval

## Publishing Notes

If you publish this skill as a standalone repository, include:

- the full skill directory
- both README files
- the `assets/` templates
- the `references/` documents

If you publish it as part of a larger repository, keep the path structure intact so relative references remain valid.
