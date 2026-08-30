# Phases

## Phase 1 - Discovery (interview)

- Lock the decision tree: settled vs WIP placement, what ships (skill / rule / templates / migrations), bundle layout, type taxonomy, frontmatter profile, agent write/query/lint protocol, agentmemory promotion, first-repo adoption.
- Verify: product-brief locked-decisions table covers every interview path. **Done 2026-08-29.**

## Phase 2 - Spec

- Write the producer profile (types, frontmatter, directory layout, write sequence, query protocol, lint) as the durable spec an implementer can follow without this interview.
- Verify: spec is in-repo; a cold-start agent pointed at it could instantiate a bundle in a greenfield repo; user has approved the spec. **Done 2026-08-29.**

## Phase 3 - Implement profile

- Skill (checklist + skeleton templates) and plan-build template updates for new trees. Do not migrate live repos in this phase.
- Verify: a new repo (or this repo) can be instantiated; `AGENTS.md` → `docs/index.md` → one concept works without agentmemory. Smoke UAT: agent updates a settled concept and a plan leaf, each refreshing the right index and log. New plan-build init uses `log.md` + frontmatter. **Done 2026-08-29.**

## Phase 4 - Adopt (optional, gated)

- Migrate a flagship repo (likely Phathom) and/or remaining plan-build trees only if Phase 1 included migration in scope.
- Verify: existing cold-start still works; no duplicate facts; monoliths unsplit unless UAT required it.

## Follow-on: skill distribution (separate effort)

- Version `okf-docs` in `skills/okf-docs/` with installer — see [okf-skill-distribution](../okf-skill-distribution/HANDOFF.md). Not a substitute for Phase 4 live-repo migration.
