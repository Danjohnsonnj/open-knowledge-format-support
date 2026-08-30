# Lessons (reusable toolkit; accreted across sessions)

## Code is the raw layer

- Context: Software-repo OKF, vs Karpathy LLM wiki / data-catalog OKF samples
- Lesson: Treat code as immutable source of truth. Concepts use `resource` / `anchor` to point at code. Authority is code > wiki > agentmemory. Do not compile a wiki *from* docs as if docs were raw.
- Evidence: Phathom `AGENTS.md` conflict resolution; OKF research 2026-08-28
- Crystallize?: yes — state in the producer profile and AGENTS.md

## Human pins must survive agent rewrites

- Context: Auto-updating concept files
- Lesson: `generated` vs `verified` stay distinct. A `human:` verification is a lock. The next ingest must not silently revert a human correction (Karpathy-scale failure mode).
- Evidence: OKF v0.2 spec §5.2–5.3; Karpathy gist comments on re-compilation
- Crystallize?: yes — write-sequence rule in the skill

## Do not split monoliths early

- Context: `CONTEXT.md`, `decisions.md` (Phathom)
- Lesson: One DecisionLog / glossary file is fine until UAT shows the monolith read is costly. Extract a term when it is cold-read often or edited in isolation.
- Evidence: Phathom `docs/agents/doc-structure.md` stop rule; assessment-doc-migration Outcome B
- Crystallize?: yes — migration stop rule in the profile

## Index-first, then 1–3 files

- Context: Token-efficient consumption
- Lesson: `AGENTS.md` and `README.md` point at `docs/index.md`; they do not contain the architecture essay. `index.md` copies `title` + `description`. Filter on folder/`type`/`status` before opening bodies.
- Evidence: OKF spec §8; this interview (minute-one discoverability)
- Crystallize?: yes — skeleton AGENTS.md/README + query protocol in the skill

## Rationale is settled, not WIP

- Context: User 2026-08-28: why A vs B may not be inferable from code
- Lesson: Locked choice-rationale belongs in Decision / Invariant concepts (settled). Open questions and deferred plans are WIP. Both corpora are first-class. Nature = type-named folder + `type` / `status`, not a `layer` key. Prefer a short updater checklist over a routing-table DSL.
- Evidence: this interview, session 1 (complexity B)
- Crystallize?: yes — profile + skill; no `layer`
