---
type: Phases
title: "OKF skill distribution phases"
description: Phase objectives and verify steps.
status: stable
generated: { by: agent/cursor, at: 2026-08-30T13:50:00Z }
---

# Phases

## Phase 1 - Import skill source

- Import `okf-docs` into `skills/okf-docs/`; consolidate producer-profile to one body.
- Verify: required skill files and templates exist; plan-tree `producer-profile.md` is a pointer only. **Done 2026-08-30.**

## Phase 2 - Installer and smoke

- Add `scripts/install-okf-docs`, `scripts/smoke-install-okf-docs`, and `SCRIPTS.md`.
- Verify: smoke script passes under temp `HOME`; ambiguous non-interactive `auto` fails safely. **Done 2026-08-30.**

## Phase 3 - Documentation and verify

- Update entry points, okf-repo-docs effort records, and logs; route `docs/index.md` to this HANDOFF.
- Verify: `./scripts/smoke-install-okf-docs`; agents install keeps plan-build sibling link working. **Done 2026-08-30.**
