---
type: DecisionLog
title: Repository decisions
description: Locked rationale that code cannot express.
status: stable
generated: { by: agent/cursor, at: 2026-08-30T14:45:00Z }
verified: { by: human:danjohnson, at: 2026-08-30T14:45:00Z }
tags: [okf, minute-one]
---

# Repository decisions

## README is human-facing; AGENTS.md is the agent pointer

**Decision:** Root `README.md` is the human landing page (GitHub, clone). Keep existing user-facing content. May add a short docs subsection linking `docs/index.md` and `AGENTS.md`. Never replace an existing README with a pointer-only stub. `AGENTS.md` is the agent minute-one pointer to `docs/index.md` (and the active `HANDOFF.md` when resuming). Query protocol prefers `AGENTS.md` when both exist.

**Rationale:** GitHub and other hosts display README by default; pointer-only READMEs fail human onboarding. Agents still need a narrow entry path without loading a fat README.

**Supersedes:** Interview decision treating both `AGENTS.md` and `README.md` as minute-one pointers / index-and-route files.
