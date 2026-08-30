# Tech brief - current state and gaps

## Current architecture (verified)

- OKF v0.2 spec — markdown + YAML frontmatter; only `type` required; reserved `index.md` (no frontmatter except root `okf_version`) and `log.md` (append-only chronology) — https://github.com/GoogleCloudPlatform/open-knowledge-format/blob/main/SPEC.md
- Phathom OKF-lite — types Glossary / Invariant / Handoff / DeliveryLog / AgentGuide; optional frontmatter including producer key `anchor`; pitfalls stay in agentmemory unless they hit twice (`docs/agents/doc-structure.md`)
- plan-build — `docs/plans/<slug>/` with HANDOFF.md (always-read, ≤50 lines), overwrite-in-place briefs, append-only `progress-log.md` (`~/.agents/skills/plan-build/`)
- okf-docs — canonical source `skills/okf-docs/` in this repo; runtime install at `~/.cursor/skills/okf-docs` and/or `~/.agents/skills/okf-docs` via `./scripts/install-okf-docs`
- research-repo / resume-work — consumers: AGENTS.md → hub → 1–3 docs
- agentmemory MCP — optional overlay; Phathom already documents “not required”

## Verified findings / gaps

1. Software repos invert Karpathy’s wiki: **code** is the immutable source, not a `raw/` folder. Wiki must lose to code on conflict. (research session 2026-08-28)
2. Phathom concept stubs (`docs/concepts/inference/with-session.md`) are already OKF-shaped; `CONTEXT.md` / `decisions.md` are monoliths without frontmatter. Stop rule: do not split until UAT shows cost.
3. plan-build `progress-log.md` is conceptually OKF `log.md` but not the reserved filename. HANDOFF.md and briefs lack frontmatter, so they fail strict bundle conformance if placed inside `docs/`.
4. v0.2 trust fields (`generated`, `verified`, `status`, `stale_after`, `sources`) are unused. They are the filter surface for “don’t load draft / stale / unverified.”
5. agentmemory is optional overlay; durable facts must live in the bundle (file-first, path gist if MCP up). (locked this interview)

## Proposed architecture

Locked. Bundle at `docs/`; type-named folders; root index Settled | In progress. Updater is a **seven-event checklist** (product-brief). `AGENTS.md` is the agent pointer to `docs/index.md`; `README.md` is human-facing (keep body; may link hub). Agentmemory: file-first, optional path gist. Skill home: `skills/okf-docs/` in this repo; install globally with `./scripts/install-okf-docs`. plan-build new trees: frontmatter + `log.md`.

Query: prefer `AGENTS.md` → `docs/index.md` → filter by folder/`type`/`status` → 1–3 files. Resume an effort: HANDOFF.md first, then required reading.

## Hard invariants

- Code > wiki > agentmemory
- `type` required on every non-reserved concept file we create going forward
- Human `verified` concepts are not overwritten without an explicit re-verify
- Next action lives only in this effort’s HANDOFF.md
