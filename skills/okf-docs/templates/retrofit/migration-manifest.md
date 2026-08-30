# {{SLUG}} migration manifest

**Target:** `{{REPO_PATH}}`
**Mapped:** {{DATE}}
**Evidence:** git history of each source path is the before-state. Do not treat this table as after-state until execution.

| Source | Disposition | Destination | Links | Rationale | Evidence |
| ------ | ----------- | ----------- | ----- | --------- | -------- |
| {{PATH}} | converted \| retained \| archived \| superseded | {{DEST_OR_DASH}} | {{WHAT_MUST_RESOLVE}} | {{ONE_SENTENCE}} | `git log -- {{PATH}}` |
