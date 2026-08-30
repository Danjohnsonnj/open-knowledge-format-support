---
name: "{{SLUG}} OKF retrofit"
overview: Assessment-only plan. Port {{REPO}} onto the software-repo OKF profile. Do not modify the target until the user approves execution.
todos:
  - id: map
    content: Index-only doc map (no body reads); wait for approval
    status: pending
  - id: classify
    content: Classify approved files one at a time into the manifest
    status: pending
  - id: after-state
    content: Propose after-state (pointers, bundle, docs-maintenance skill)
    status: pending
  - id: execute
    content: BLOCKED until user approves this plan — then port per manifest
    status: pending
isProject: false
---

# {{SLUG}} OKF retrofit

**Target:** `{{REPO_PATH}}` (do not write here during assessment)

**Manifest:** [{{SLUG}}-okf-retrofit-manifest.md]({{SLUG}}-okf-retrofit-manifest.md)

**Profile:** `~/.agents/skills/okf-docs/producer-profile.md`

## Assessment notes

{{MAP_SUMMARY}}

## Proposed after-state

- Minute-one: `AGENTS.md` / `README.md` → `docs/index.md`
- Bundle indexes + `docs/log.md`
- Repo-local `.cursor/skills/docs-maintenance/` (extensions and exceptions only)
- Port per manifest; path is identity unless a row says otherwise

## Out of scope until execution is approved

Any write to `{{REPO_PATH}}`.
