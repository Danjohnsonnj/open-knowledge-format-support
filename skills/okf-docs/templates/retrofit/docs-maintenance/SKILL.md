---
name: docs-maintenance
description: Repo-specific OKF documentation rules. Use when updating this repo's docs/, wrapping up a session, or applying the seven-event checklist. Defers shared protocol to the global okf-docs skill.
---

# Docs maintenance ({{PROJECT}})

Repo-local overlay. Shared protocol: global `okf-docs` (producer profile, checklist, routing, on-write). This file holds **only** what is unique to this repo.

## Authority

code > `docs/` > agentmemory

{{AUTHORITY_EXCEPTIONS_OR_DELETE}}

## Type-folder extensions

Default folders/types are in the producer profile. This repo also allows:

{{EXTRA_FOLDERS_AND_TYPES_OR_NONE}}

## Commands (doc-adjacent)

{{DOC_COMMANDS_OR_DELETE}}

## Code anchors

{{PATHS_AGENTS_SHOULD_POINT_RESOURCE_AT}}

## Migration exceptions

{{RETAINED_OR_ARCHIVED_PATHS_AND_WHY}}
