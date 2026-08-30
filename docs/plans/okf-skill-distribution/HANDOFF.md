---
type: Handoff
title: "OKF skill distribution handoff"
description: "Version the okf-docs skill in-repo and install it to Cursor or agent skill roots."
status: stable
generated: { by: agent/cursor, at: 2026-08-30T13:50:00Z }
---

# OKF skill distribution - Handoff

**Goal:** Make this repository the versioned canonical source for the `okf-docs` skill, with a safe installer for Cursor and agent skill roots.

**Current phase:** Phase 3 — Documentation and verify — complete
**Next action:** None. Run `./scripts/install-okf-docs` on a new machine when global skill roots are needed.

**Hard invariants:** `skills/okf-docs/` is the only editable producer-profile body. Do not commit unless asked. Preserve global installs until smoke checks pass.

**Required reading (this phase):**

- docs/plans/okf-skill-distribution/lessons.md — toolkit; reuse before re-deriving
- docs/plans/okf-skill-distribution/tech-brief.md — source vs install targets
- docs/plans/okf-skill-distribution/process.md — read before any commit request

**Index (load on demand):** product-brief.md · tech-brief.md · phases.md · process.md · log.md · lessons.md

**Open decisions:** None
**Last updated:** 2026-08-30 — skill re-homed; installer and docs updated
