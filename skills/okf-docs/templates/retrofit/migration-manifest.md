# {{SLUG}} migration manifest

**Target:** `{{REPO_PATH}}`
**Mapped:** {{DATE}}
**Evidence:** git history of each source path is the before-state. Do not treat this table as after-state until execution.

Candidate set = every legacy path from the user-approved gate-1 map (exhaustive). One row per path; no unlisted paths.

| Source | Disposition | Confidence | Destination | Links | Rationale | Evidence |
| ------ | ----------- | ---------- | ----------- | ----- | --------- | -------- |
| {{PATH}} | converted \| retained \| archived \| superseded | high \| ask | {{DEST_OR_DASH}} | {{WHAT_MUST_RESOLVE}} | {{ONE_SENTENCE}} | `git log -- {{PATH}}` |

**Disposition:** `converted` | `retained` | `archived` | `superseded`

**Confidence:** `high` = safe to execute as proposed; `ask` = needs user decision before execution. Uncertain rows default to `retained` + `ask`, not invented `converted`.
