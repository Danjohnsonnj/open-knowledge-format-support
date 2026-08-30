---
type: Lesson
title: "OKF skill distribution lessons"
description: Curated toolkit of reusable gotchas and verify outcomes.
status: draft
generated: { by: agent/cursor, at: 2026-08-30T13:50:00Z }
---

# Lessons (reusable toolkit; accreted across sessions)

## Repo is source; globals are install targets

- Context: okf-docs skill distribution
- Lesson: Edit `skills/okf-docs/` in this repository. Install to `~/.cursor/skills/okf-docs` and/or `~/.agents/skills/okf-docs` with `./scripts/install-okf-docs`. Do not treat global copies as canonical after re-home.
- Evidence: product-brief installer policy; tech-brief install targets
- Crystallize?: yes — AGENTS.md and SCRIPTS.md

## plan-build sibling layout

- Context: plan-build references `../okf-docs/producer-profile.md` relative to its install directory
- Lesson: When both skills live directly under `~/.agents/skills/`, agents-target install satisfies the sibling link. If plan-build is symlinked elsewhere (e.g. to a monorepo of skills), also install or link `okf-docs` next to plan-build's resolved target.
- Evidence: nominal `~/.agents/skills/{plan-build,okf-docs}` layout resolves; symlinked plan-build may not use `~/.agents/skills/okf-docs`
- Crystallize?: no

## Smoke tests need isolated HOME

- Context: installer verification
- Lesson: Run `./scripts/smoke-install-okf-docs` before trusting an install script; it uses a temp `HOME` so real skill roots are untouched.
- Evidence: smoke script passes after per-case symlink assertions
- Crystallize?: yes — SCRIPTS.md
