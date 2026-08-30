# Product brief - OKF repo documentation

## Background

Project documentation today is split across `AGENTS.md`, `README.md`, glossary/decision monoliths, plan-build handoff trees, and optional agentmemory. That works locally and fails for cloud agents or any workspace without MCP. Google’s Open Knowledge Format (OKF) v0.2 formalizes the LLM-wiki pattern: a directory of markdown concepts with YAML frontmatter, reserved `index.md` / `log.md`, and progressive disclosure so an agent loads only what it needs. Phathom already runs an “OKF-lite” profile. This effort turns that into the default documentation foundation for every repo.

## Goal

A reusable, OKF-compatible documentation process: both **settled knowledge** and **WIP** (open questions, deferred plans, in-flight efforts) are primary use cases. Nature is obvious from **type-named folders** plus queryable frontmatter (`type`, `status`) so an agent can load either corpus on purpose without mixing them. Locked rationale that code cannot express is settled knowledge (Decision), not WIP.

## Rationale

Cloud agents and fresh workspaces cannot see agentmemory. Token spend is wasted when agents dump monoliths. Knowledge that only exists in chat or MCP is not durable. OKF gives a vendor-neutral shape; we need a producer profile and a maintenance ritual tailored to software repos (code is source of truth; the wiki describes it).

## Non-goals

- Building a search service, visualizer, or Knowledge Catalog analog
- Requiring Google’s reference agent or any OKF SDK
- Splitting large existing monoliths (`CONTEXT.md`, `decisions.md`) until UAT shows they are costly
- Attested Computation / metric attestation (defer until a repo has numbers an agent must not improvise)
- Migrating every existing repo in the first delivery (scope to be locked in interview)

## Boundaries

- Always: code wins over wiki; human-verified concepts are not silently regenerated; `log.md` / progress logs are append-only; do not commit unless asked
- Ask first: migrating a live repo; promoting agentmemory pitfalls into the bundle
- Never: duplicate the same fact in AGENTS.md, a glossary, and a stub; put the architecture essay in AGENTS.md or README; put secrets in the bundle; treat agentmemory as authoritative over repo docs

## Success criteria

- A cold-start agent in a workspace without agentmemory can load `AGENTS.md` → `docs/index.md` → 1–3 concepts and act
- Settled vs WIP are distinguishable without reading bodies (path under `plans/` vs not, plus `type` / `status`)
- Both corpora are first-class in the root index; loading one does not require loading the other
- An agent can add/update a concept, refresh the affected index, and append the log in one pass
- New repos can adopt the profile without a custom one-off design

## Locked decisions (interview)

- **Settled knowledge** and **WIP** are both primary use cases.
- **Layout:** type-named folders at `docs/` with equal root-index sections (Settled | In progress).
- **Default shared set:** Settled — `docs/concepts/` (`Glossary`, `Invariant`, `Module`, `Architecture`), `docs/runbooks/` (`Runbook`, `Playbook`), `docs/agents/` (`AgentGuide`, `ProductState`), one `docs/decisions.md` (`DecisionLog`) until UAT says split. WIP — only `docs/plans/<slug>/`. Bundle root `docs/index.md` + `docs/log.md`. No default `questions/` or `layer` key. Extra type folders are per-repo extensions. `docs/archive/` optional.
- **Complexity (B):** keep those splits; drop duplicates. No `layer`. No formal routing-table DSL. No 4-way lint.
- **Frontmatter required:** `type`, `title`, `description`, `status`, `generated`. Recommended: `tags`, `resource`. When locking an invariant/decision: `verified`. Optional: `stale_after`, `sources`, `anchor`. Nature = folder family + `type`. `status` = document readiness (a HANDOFF may be `stable` and still WIP).
- **Minute-one:** `AGENTS.md` is the agent pointer to `docs/index.md` (and the active HANDOFF when resuming). `README.md` is the human landing page — keep user-facing content; may link the hub. Neither holds the architecture essay.
- **Updater checklist (seven events):**
  1. Decision or invariant locked → `docs/decisions.md` (`verified` when locked).
  2. Ship / defer / priority change → `docs/agents/` ProductState.
  3. Domain term now in code or issue titles → `docs/concepts/` Glossary stub.
  4. Ops path we actually run → `docs/runbooks/`.
  5. Durable agent obligation → `docs/agents/`.
  6. Session wrap, open question, deferred work, or in-flight design → current `docs/plans/<slug>/`.
  7. Architecture, dependency **policy**, or a coding/ops pattern locked → `docs/concepts/` as `Architecture`, `Module`, or `Invariant`. Lockfiles/code remain source of truth for versions. One concern per file; do not grow a new monolith.
- **Routing rules (still apply):** exact checklist hit → write there. Existing file → stay put. New settled without a hit → ask. Other new files → `draft` in the current plan tree. Never invent a settled page.
- **Never:** put the architecture essay in `AGENTS.md` or `README.md`; `AGENTS.md` routes agents, `README.md` serves humans on GitHub.
- **Lint:** `docs/plans/**` is WIP; other default folders are settled; `type` must be in that folder’s allowed set.
- **Settle:** write the settled file and link from the plan. Deprecate the WIP copy only when it would still look current. Do not move files (path is identity).
- **Delivery (C):** this effort ships (1) a global skill with a short updater checklist and a new-repo skeleton in `templates/`, (2) plan-build template updates for *new* trees (frontmatter on leaves; effort `log.md` instead of `progress-log.md`; `docs/plans/` is the WIP side of the bundle). Old plan trees stay until touched. Live-repo migration is a later gated phase, not v1.
- **Agentmemory (A):** bundle is the write. Architecture / preferences / locked rationale go to the matching file first. If MCP is up, save a **path-only gist**, not a body paste. Pitfalls stay in memory until they hit twice, then a `Lesson` (settled `concepts/` if locked, else current plan). Missing MCP is not a failure.
- **Skill home (v1):** shipped globally alongside plan-build; skeleton in the skill’s `templates/`.
- **Skill home (current):** canonical source is `skills/okf-docs/` in this repository; install to global roots with `./scripts/install-okf-docs` (see [okf-skill-distribution](../okf-skill-distribution/HANDOFF.md)).
- **Why A vs B** (choice rationale) is a settled Decision, not WIP.
- Default task load stays narrow: pick the corpus the task needs.
