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
2. **Summarize.** Bullet the top candidates. Stop and wait for approval.
3. **Classify one approved document at a time** (now reading that body). Update the manifest row. Do not batch-classify in one turn.

If the index pass finds no doc candidates, say so and stop.

## Manifest row

Every discovered legacy file gets one row:

| Column | Values |
| ------ | ------ |
| Source | path in the target repo |
| Disposition | `converted` \| `retained` \| `archived` \| `superseded` |
| Destination | proposed OKF path, or `—` |
| Links | what must keep resolving |
| Rationale | one sentence |
| Evidence | git path / history note (before-state) |

Do not guess dispositions without reading the approved file.

## Proposed after-state (in the local plan, not the repo)

- Root `AGENTS.md` / `README.md` pointers to `docs/index.md`
- Bundle: `docs/index.md`, `docs/log.md`, folder indexes
- Incremental port per manifest (settle-without-move: path is identity; do not invent moves as the default)
- Repo-local `.cursor/skills/docs-maintenance/` from the template (authority order, type-folder extensions, commands, code anchors, migration exceptions). Link to global `okf-docs`.

On **approved execution** (separate from this assessment run): replace/move sources into the OKF structure per the manifest. That write is out of this assessment run.

## Local plan skeleton

Copy [templates/retrofit/retrofit-plan.md](templates/retrofit/retrofit-plan.md) and [templates/retrofit/migration-manifest.md](templates/retrofit/migration-manifest.md). Fill YAML todos that an executor can run without this chat.

## Verify (assessment)

- Manifest covers every file from the approved map.
- Proposed links are bundle-relative and would resolve after execution.
- `git status` / `git diff` in the **target** is unchanged by the assessment.
