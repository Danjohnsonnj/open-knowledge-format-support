# Producer profile — software-repo OKF

Implementer spec for an OKF v0.2–compatible documentation bundle in a git repo. Rationale and locked interview decisions: [product-brief.md](../../docs/plans/okf-repo-docs/product-brief.md). Format rules this profile does not restate: [OKF v0.2 SPEC](https://github.com/GoogleCloudPlatform/open-knowledge-format/blob/main/SPEC.md).

**Authority:** code > this bundle > agentmemory. On conflict, fix the wiki or ignore it; do not “correct” code from docs.

A cold-start agent can instantiate a greenfield bundle from this file plus the [Greenfield instantiate](#greenfield-instantiate) checklist. For an existing repo with legacy docs but no `docs/index.md`, use global `okf-docs` **Retrofit** mode ([retrofit.md](retrofit.md)) — assessment procedure lives there, not here.

## Bundle root

Bundle root is `docs/` at the repository root (not the git root as the OKF bundle — the repo *contains* the bundle).

| Reserved file | Rules |
| ------------- | ----- |
| `docs/index.md` | Directory listing. No frontmatter except optional `okf_version: "0.2"` at **bundle root only**. Sections **Settled** and **In progress**. Entries copy `title` + `description` from the linked file (or the folder index’s heading + one-liner). |
| `docs/log.md` | Append-only chronology for the bundle. Date headings `YYYY-MM-DD`. **Newest first** (OKF §9). |

Do not use `index.md` or `log.md` as concept filenames. Folder-level `index.md` / `log.md` MAY exist; only the root index may set `okf_version`.

Concept ID = path relative to `docs/` with `.md` stripped (OKF §2). **Path is identity — never move a file to “settle” it.**

## Folder map and types

Nature = **folder family + `type`**. No `layer` key. Extra type folders are per-repo extensions (declare them in repo-local docs-maintenance when that skill exists). `docs/archive/` is optional.

### Settled (default folders other than `plans/`)

| Path | Allowed `type` |
| ---- | -------------- |
| `docs/concepts/` | `Glossary`, `Invariant`, `Module`, `Architecture`, `Lesson` (locked) |
| `docs/runbooks/` | `Runbook`, `Playbook` |
| `docs/agents/` | `AgentGuide`, `ProductState` |
| `docs/decisions.md` | `DecisionLog` — **one file** until UAT shows the monolith is costly |

Create `docs/decisions.md` on the first Decision event; do not put an empty stub in the new-repo skeleton.

Each settled type folder has an `index.md` (no frontmatter). Root **Settled** links those indexes (and `decisions.md` once it exists), not every leaf.

### WIP (only `docs/plans/<slug>/`)

One effort tree per slug. Leaf types for **new** trees (plan-build templates):

| Leaf | `type` |
| ---- | ------ |
| `HANDOFF.md` | `Handoff` |
| `product-brief.md` | `ProductBrief` |
| `tech-brief.md` | `TechBrief` |
| `phases.md` | `Phases` |
| `process.md` | `Process` |
| `log.md` | `DeliveryLog` |
| `lessons.md` | `Lesson` (still WIP) |

`HANDOFF.md` uses `status: stable` (readiness) even though the effort is WIP (folder is nature).

**Legacy trees** keep `progress-log.md` and no frontmatter until touched. If `log.md` is absent, append to `progress-log.md`.

Root **In progress** lists each effort as a link to its `HANDOFF.md`.

## Frontmatter

OKF requires only `type`. **This profile requires** on every new non-reserved concept:

```yaml
---
type: Glossary
title: Display name
description: One sentence for indexes and previews.
status: draft          # draft | stable | deprecated
generated: { by: agent/model-or-human:id, at: 2026-08-29T13:00:00Z }
# recommended
tags: [okf]
resource: /path/or-uri-to-code   # when the concept describes code
# when locking an invariant or decision
verified: { by: human:id, at: 2026-08-29T13:00:00Z }
# optional
stale_after: 2027-02-01T00:00:00Z
sources: []
anchor: optional-producer-key    # in-repo code pointer beyond resource
---
```

| Field | Meaning |
| ----- | ------- |
| `type` | Kind. Must be in the folder’s allowed set. |
| `status` | **Document readiness**, not settled vs WIP. Absent ⇒ `stable` (OKF). A stable Handoff can still live under `plans/`. |
| `generated` | Who last wrote the body (`by` + `at`). Distinct from `verified`. |
| `verified` | Confirmation. Set when locking an invariant or decision. `human:` prefix = human-reviewed (OKF §5.3, §7). |

**Human pin:** do not overwrite a `verified` `human:` concept without an explicit re-verify. Update `generated` on rewrite; do not drop `verified` silently.

Reserved files (`index.md`, `log.md`) are not concepts — do not add `type`.

## Minute-one files

Different audiences. Neither file is the architecture essay.

- `AGENTS.md`: **agent pointer** — one-line purpose, stack/commands stubs, link to `docs/index.md`. When resuming a named effort, also point at that effort’s `HANDOFF.md`.
- `README.md`: **human landing page** (GitHub, clone). Keep user-facing content (install, usage, license, screenshots). May add a short docs subsection linking `docs/index.md` (and `AGENTS.md` if present). Never replace an existing README with a pointer-only stub. Greenfield seed may be short (purpose + hub link) because there is no prior GitHub copy.

Never duplicate a glossary, decision, or architecture write-up in either file. Never put secrets in the bundle.

## Query protocol

Default load is narrow. Pick the corpus the task needs (settled **or** WIP), not both.

1. Read `AGENTS.md` when it exists; otherwise `README.md`. Do not load a fat README as the first hop when `AGENTS.md` is present.
2. Open `docs/index.md`. Filter by section (Settled / In progress), then folder, `type`, and `status`.
3. Open **1–3** files. Stop.

**Resume an effort:** open that effort’s `HANDOFF.md` first, then only leaves listed under its “Required reading (this phase).” Do not start at `docs/index.md` and browse into the plan.

Consumers (`research-repo`, `resume-work`): treat `docs/index.md` as the doc hub when present.

## Seven-event checklist

On a matching event, write the matching file. One concern per file.

| # | Event | Write |
| - | ----- | ----- |
| 1 | Decision or invariant locked | `docs/decisions.md` (`DecisionLog`). Set `verified` when locked. Why A vs B is a Decision, not WIP. |
| 2 | Ship / defer / priority change | `docs/agents/` `ProductState` |
| 3 | Domain term now in code or issue titles | `docs/concepts/` `Glossary` stub |
| 4 | Ops path we actually run | `docs/runbooks/` (`Runbook` or `Playbook`) |
| 5 | Durable agent obligation | `docs/agents/` (`AgentGuide`) |
| 6 | Session wrap, open question, deferred work, or in-flight design | current `docs/plans/<slug>/` |
| 7 | Architecture, dependency **policy**, or a coding/ops pattern locked | `docs/concepts/` as `Architecture`, `Module`, or `Invariant`. Lockfiles/code remain source of truth for versions. |

## Routing

1. **Hit** — event matches the checklist → write there.
2. **Stay put** — a file for this concern already exists → update it; do not create a sibling.
3. **Ask** — new **settled** page with no checklist hit → ask the user; never invent a settled page.
4. **WIP default** — any other new file → `status: draft` in the current plan tree.

## On-write

In the same pass as the concept edit:

1. Refresh the **folder** `index.md` that lists the file (`title` + `description`).
2. If the file is newly added to the bundle’s top-level map, refresh **`docs/index.md`**.
3. Append **`docs/log.md`** (newest first).
4. If the file is under `docs/plans/<slug>/`, also append that effort’s `log.md`, or `progress-log.md` when `log.md` is absent.

Do not commit unless asked.

## Lint (agent-enforced; no script in v1)

- `docs/plans/**` is WIP; other default folders are settled.
- `type` ∈ that folder’s allowed set.
- `AGENTS.md` indexes only; `README.md` stays human-facing (may link the hub).
- No `layer` key. No default `docs/questions/`.
- Do not split `docs/decisions.md` or a glossary monolith without task-level UAT evidence.

## Settle without move

Path is identity. To promote WIP → settled:

1. Write the settled file in the correct folder with required frontmatter.
2. Link to it from the plan leaf that used to hold the fact.
3. Deprecate the WIP copy **only if it would still look current** (`status: deprecated` or a one-line “superseded by”).
4. Do **not** move or rename the WIP file into a settled folder.

## File-first memory

The bundle is the write. Architecture, preferences, and locked rationale go to the matching file first.

If agentmemory MCP is up, save a **path-only gist** (link + one-line), not a body paste. Missing MCP is not a failure.

Pitfalls stay in memory until they hit **twice**, then a `Lesson`: settled `docs/concepts/` if locked, else the current plan’s `lessons.md`.

## Greenfield instantiate

Create only these files (no architecture essay, no empty `decisions.md`, no plan tree until plan-build init):

```
AGENTS.md                 # agent pointer: purpose, commands/stack stubs, link to docs/index.md
README.md                 # human landing: purpose + hub link (expand as the product needs)
docs/index.md             # okf_version: "0.2"; Settled | In progress
docs/log.md               # empty dated log (heading only is fine)
docs/concepts/index.md
docs/runbooks/index.md
docs/agents/index.md
```

Verify: `AGENTS.md` → `docs/index.md` → at most 1–3 files. A cold-start agent with no agentmemory can follow that path.

## Out of this profile (v1)

Live-repo migration, retrofit of existing plan-tree frontmatter, lint script, `layer`, default `questions/`, Attested Computation, Google reference agent, visualizer, catalog/RAG/search service.
