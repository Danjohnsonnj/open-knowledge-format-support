---
type: Invariant
title: Code wins over wiki
description: On conflict, code is source of truth; fix or ignore the wiki.
status: stable
generated: { by: agent/cursor-grok-4.6, at: 2026-08-29T13:45:00Z }
tags: [okf, authority]
---

# Code wins over wiki

Software-repo OKF inverts data-catalog OKF: **code** is the immutable source, not a `raw/` folder.

On conflict: fix the wiki or ignore it. Do not “correct” code from docs. Concepts that describe code use `resource` / `anchor` to point at it.

Authority: code > `docs/` > agentmemory.
