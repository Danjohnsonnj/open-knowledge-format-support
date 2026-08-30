---
name: "{{SLUG}} OKF retrofit"
overview: Assessment-only plan. Port {{REPO}} onto the software-repo OKF profile. Do not modify the target until the user approves execution.
todos:
  - id: map
    content: Index-only pass; write delta header + Before/After trees + change table + Confirm extras into MAP_SUMMARY; wait for user approval
    status: pending
  - id: classify
    content: Use approved gate-1 candidate set; bulk-read all bodies; fill manifest with disposition + Confidence; present review sheet and wait; apply user answers to affected rows only; present resolved sheet; execution blocked until separately approved
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

## Structure gut-check (gate 1 — approved map)

{{MAP_SUMMARY}}

Paste here when gate 1 runs (same content as chat):

1. **Delta header** — `Proposed adds: … Moves: … Extras to confirm: …`
2. **Before (today)** — compressed tree with missing OKF pieces called out
3. **After (proposed — mostly additive)** — tagged tree (`[+]`, `[=]`, `[~]`, `[?]`)
4. **What changes vs what stays** — short table
5. **Confirm** — yes/no for each `[?]` extra folder
6. **Candidate bullets** — top legacy paths for classify

Path is identity. Nothing classified until the user approves this section.

## Classification review (gate 2 — approved manifest)

After gate 1 approval, bulk-classify every candidate path into the manifest. Present the review sheet in chat (counts, by-disposition lists, Needs a decision, review prompt). Wait for user answers; update only affected rows; present the resolved sheet. Execution remains blocked until separately approved.

## Proposed after-state

Same as the approved **After** tree above. During classify, bulk-fill manifest rows then resolve user answers; do not re-invent structure.

- Minute-one: `AGENTS.md` → `docs/index.md`; `README.md` stays human-facing (append hub link if missing)
- Bundle indexes + `docs/log.md` (no empty `docs/decisions.md`)
- Repo-local `.cursor/skills/docs-maintenance/` (extensions and exceptions only)
- Port per manifest; path is identity unless a row says otherwise

## Out of scope until execution is approved

Any write to `{{REPO_PATH}}`.
