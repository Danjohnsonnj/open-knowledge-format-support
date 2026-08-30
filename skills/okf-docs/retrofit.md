# OKF retrofit (assessment only)

Assess an existing repo against the software-repo OKF profile. **Terminal condition:** an executable local plan plus a migration manifest under `~/.cursor/plans`. **Never modify the target repo during assessment.**

Profile: [producer-profile.md](producer-profile.md). Execution (after the user approves the local plan) follows [SKILL.md](SKILL.md) (Maintain/Init modes) and installs [templates/retrofit/docs-maintenance/SKILL.md](templates/retrofit/docs-maintenance/SKILL.md) into the repo as `.cursor/skills/docs-maintenance/`.

## Outputs

Write only under `~/.cursor/plans/`:

| File | Purpose |
| ---- | ------- |
| `<slug>-okf-retrofit.plan.md` | Cursor plan: todos for approved execution |
| `<slug>-okf-retrofit-manifest.md` | Every legacy doc → disposition |

`<slug>` = repo directory name, kebab-case.

## Research gate (Code Audits)

Do not skip. Do not classify until the user approves the map.

1. **Index-only.** Glob / file-tree the target. List candidate docs (`AGENTS.md`, `README.md`, `CONTEXT.md`, `docs/**`, `.github` agent files, skill docs). **Do not read bodies.**
2. **Structure gut-check.** Propose a **before/after** docs tree (structure only — nothing classified yet). Write the same content in chat **and** in `{{MAP_SUMMARY}}` on the local plan. **Stop and wait for approval.**
3. **Bulk classify + review sheet.** After map approval, read every body in the **approved gate-1 candidate set** (exhaustive — do not silently add paths; if a new path must be included, stop and request a map update). Write the full manifest to `~/.cursor/plans/<slug>-okf-retrofit-manifest.md` using [templates/retrofit/migration-manifest.md](templates/retrofit/migration-manifest.md). Present the **review sheet** in chat. **Stop and wait for approval.**

If the index pass finds no doc candidates, say so and stop.

### Step 2 output (required)

Path is identity. Existing paths stay unless a later manifest row says otherwise. Do not read bodies in this step.

**A. Delta header (one line, read first)**

`Proposed adds: … Moves: none|…. Extras to confirm: …`

If **Moves** is not `none`, the map is wrong unless the user already asked for moves (default is settle-without-move).

**B. Before (today)** — compressed tree. Show docs-adjacent surface only:

- Repo root: minute-one files (`AGENTS.md`, `README.md`, `CONTEXT.md` if present).
- `docs/` with **missing** OKF pieces called out inline (`← no index.md`, `← no log.md`, etc.).
- One `[=]` line each for clearly non-bundle dirs (`spike/`, `src/`, `assets/`) so they are not swallowed.
- Collapse leaves: `…existing…`, `*.md`. Do not expand application code.

**C. After (proposed — mostly additive)** — same scope, additive skeleton only:

- `[+]` new OKF-required nodes (hub, log, folder indexes, `AGENTS.md` if missing, `docs-maintenance` skill).
- `[=]` keep path.
- `[~]` keep path but change only as noted (`AGENTS.md` → pointer to `docs/index.md`; `README.md` → append hub/docs subsection if missing — **never** strip to pointer-only).
- `[?]` extra / ambiguous folder (needs Confirm answer).
- Do **not** add `docs/decisions.md` or concept leaves. Do **not** rename `progress-log.md` here.

**Line tags:** `[+]` `[=]` `[~]` `[?]` — scan without reading inline comments. Do not put `converted` / `archived` on the tree (those are manifest rows after approval).

**D. What changes vs what stays** — 5–8 row table (required adds, AGENTS pointer, README human-facing / optional hub append, extras, explicit non-goals).

**E. Confirm** — max ~5 yes/no questions for each `[?]` extra `docs/` folder: Settled (folder `index.md` + docs-maintenance) | outside Settled | archive-later. Approval of the map includes those answers.

**F. Candidate bullets** — short list of top legacy doc paths from the index pass (feeds step 3).

Footnote when relevant: `docs/decisions.md` is **not** created empty; it appears on the first locked decision.

#### Compact example

```text
Proposed adds: AGENTS.md, docs/index.md, docs/log.md, 3 folder index.md, docs-maintenance skill. Moves: none. Extras to confirm: design-mocks/

### Before (today)

my-app/
├── README.md
├── src/                           [=] not the bundle
└── docs/                          ← no index.md, no log.md
    ├── runbooks/
    │   ├── README.md              ← not an OKF folder index
    │   └── …existing…
    └── plans/my-app/
        └── progress-log.md        ← legacy log name

### After (proposed — mostly additive)

my-app/
├── [+] AGENTS.md
├── [~] README.md                    KEEP body; add hub link if missing
├── [=] src/
├── [+] .cursor/skills/docs-maintenance/
└── docs/
    ├── [+] index.md
    ├── [+] log.md
    ├── concepts/
    │   └── [+] index.md
    ├── runbooks/
    │   ├── [+] index.md
    │   ├── [=] README.md          until classified
    │   └── [=] …existing…
    ├── plans/my-app/              [=] WIP tree
    │   └── [=] progress-log.md    keep name until touched
    └── [?] design-mocks/          Confirm: Settled | outside | archive-later
```

Invite the user to reject extras or request a different after-state when approving the map.

### Step 3 output (required)

Do not guess dispositions without reading the approved file. Assessment writes only under `~/.cursor/plans/` — never the target repo.

**A. Full manifest** — one row per approved-map candidate. Every row needs a valid disposition and `Confidence: high | ask`. Uncertain rows: `retained` + `ask`, not invented `converted`.

**B. Review sheet (chat primary UI)** — not the raw table:

1. **Counts** — disposition counts (`N converted · M retained · K superseded · J archived`) plus `Q Confidence: ask` rows
2. **By disposition** — path lists; one line each: `path · dest or — · one-clause why`
3. **Needs a decision** — numbered A/B (or A/B/C) for each `ask` row or real fork; cluster by folder if more than ~8 questions (e.g. `docs/design-mocks/*`)
4. **Review prompt** — accept all `high` rows as proposed; answer every `ask` question; or name path overrides. No `ask` row proceeds to execution until resolved or explicitly left as `retained` by the user.

Do not paste monolith bodies (`CONTEXT.md`) into chat; one-sentence rationale + destination only.

**C. After user responds** — update only affected manifest rows, recompute counts, present the **resolved sheet**, then **stop** again for separate execution approval. Do not re-read or reclassify unchanged files. Do not re-print the after-tree unless a row proposes a real move or archive.

**D. Do not batch-execute.** Porting the target repo is a separate step after the resolved manifest is approved.

## Manifest row

Every discovered legacy file gets one row:

| Column | Values |
| ------ | ------ |
| Source | path in the target repo |
| Disposition | `converted` \| `retained` \| `archived` \| `superseded` |
| Confidence | `high` \| `ask` — required on every row; `ask` = needs user decision before execution |
| Destination | proposed OKF path, or `—` |
| Links | what must keep resolving |
| Rationale | one sentence |
| Evidence | git path / history note (before-state) |

Do not guess dispositions without reading the approved file. The approved gate-1 candidate set is exhaustive.

## Proposed after-state (in the local plan, not the repo)

The step 2 trees **are** the after-state proposal. Do not invent a second after-state after classify.

- Record the approved trees in `{{MAP_SUMMARY}}` when the user approves the map (gate 1).
- During classify, update **manifest rows** only (bulk pass, then resolved sheet after user answers). Re-print an after tree only if a row proposes a real move or archive (rare).
- Skeleton contents: `AGENTS.md` pointer to `docs/index.md`; `README.md` human-facing (keep body; append hub link if missing); bundle `docs/index.md`, `docs/log.md`, folder indexes; incremental port per manifest (settle-without-move); repo-local `.cursor/skills/docs-maintenance/` from the template (authority order, type-folder extensions, commands, code anchors, migration exceptions). Link to global `okf-docs`.

On **approved execution** (separate from this assessment run): replace/move sources into the OKF structure per the manifest. That write is out of this assessment run.

## Local plan skeleton

Copy [templates/retrofit/retrofit-plan.md](templates/retrofit/retrofit-plan.md) and [templates/retrofit/migration-manifest.md](templates/retrofit/migration-manifest.md). Fill YAML todos that an executor can run without this chat.

## Verify (assessment)

- Every approved-map candidate has exactly one manifest row; no unlisted path is classified.
- Every row has a valid disposition and `Confidence: high | ask`; no unresolved `ask` row proceeds to execution.
- Proposed links are bundle-relative and would resolve after execution.
- `git status` / `git diff` in the **target** is unchanged by the assessment.
