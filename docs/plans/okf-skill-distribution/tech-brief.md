---
type: TechBrief
title: "OKF skill distribution tech brief"
description: Source tree, install targets, and verification for okf-docs distribution.
status: stable
generated: { by: agent/cursor, at: 2026-08-30T13:50:00Z }
---

# Tech brief - current state and gaps

## Current architecture (verified)

- **Canonical source:** `skills/okf-docs/` — `SKILL.md`, `producer-profile.md`, `retrofit.md`, `templates/`
- **Installer:** `scripts/install-okf-docs` — copy or symlink to global roots
- **Smoke:** `scripts/smoke-install-okf-docs` — temp-`HOME` verification
- **Command reference:** `SCRIPTS.md`
- **Plan-tree pointer:** `docs/plans/okf-repo-docs/producer-profile.md` links to the skill copy only

## Install targets

| Target | Path |
| ------ | ---- |
| Cursor | `~/.cursor/skills/okf-docs` |
| Agents | `~/.agents/skills/okf-docs` |

Default mode is `copy` (portable). Use `link` for local iteration against the repo source.

## Verified findings / gaps

1. Global `~/.cursor/skills/okf-docs` and `~/.agents/skills/okf-docs` were identical at import time.
2. plan-build still resolves `../okf-docs/producer-profile.md` relative to its global install; agents-target install must keep that sibling link working.
3. Workspace-local `.cursor/skills/okf-docs` inside this repo is out of scope; clone uses the installer.

## Hard invariants

- Edit the skill only under `skills/okf-docs/`
- Installer must not silently pick a target when `auto` is ambiguous in non-interactive use
- Do not overwrite a non-symlink destination without `--replace`
