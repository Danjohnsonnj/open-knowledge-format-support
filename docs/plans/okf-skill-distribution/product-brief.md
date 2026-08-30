---
type: ProductBrief
title: "OKF skill distribution product brief"
description: Goals, rationale, non-goals, and boundaries for in-repo skill distribution.
status: stable
generated: { by: agent/cursor, at: 2026-08-30T13:50:00Z }
---

# Product brief - OKF skill distribution

## Background

v1 shipped `okf-docs` only under global skill roots (`~/.cursor/skills/`, `~/.agents/skills/`). The producer profile and templates were not versioned with this repository, so spec and skill could drift.

## Goal

This repository is the canonical, versioned source for `okf-docs`. Contributors edit `skills/okf-docs/`; environments install from it via `scripts/install-okf-docs`.

## Rationale

- Reviewable skill changes in the same repo as the OKF profile design
- Reproducible installs on new machines without hand-copying from home directories
- Clear separation: repo = source, global roots = runtime install targets

## Non-goals

- Vendoring `okf-docs` into every software repository (retrofit still installs repo-local `docs-maintenance` only)
- Live-repo OKF migration (gated Phase 4 of okf-repo-docs)
- Redesigning plan-build to load the profile from this repo instead of a sibling global install

## Boundaries

- Always: one editable `producer-profile.md` body under `skills/okf-docs/`; do not commit unless asked
- Ask first: overwriting a user's global install without `--replace`
- Never: treat `~/.agents/skills/okf-docs` as the authoritative edit surface after re-home

## Success criteria

- `skills/okf-docs/` contains the full skill and templates
- `./scripts/smoke-install-okf-docs` passes under a temp `HOME`
- Entry points and HANDOFF route cold-start agents to the in-repo source and installer
- Installer supports `--target cursor|agents|both|auto` and `--mode copy|link`

## Installer policy (locked)

| Option | Values | Default |
| ------ | ------ | ------- |
| `--target` | `cursor`, `agents`, `both`, `auto` | `auto` |
| `--mode` | `copy`, `link` | `copy` |
| `--replace` | flag | off |

`auto` uses the sole existing install or sole existing skills parent; when both or neither apply, prompt interactively or require an explicit `--target`.
