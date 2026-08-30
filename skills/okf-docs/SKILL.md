---
name: okf-docs
description: Initializes and maintains an OKF-compatible docs/ bundle in a software repo. Use when creating repo docs, wrapping up a session, locking a decision or invariant, updating product state, adding a glossary/runbook/agent guide, retrofitting or migrating legacy docs (CONTEXT.md, monoliths) onto the OKF profile, or when the user mentions OKF, docs/index.md, documentation maintenance, or OKF retrofit.
---

# OKF docs

## Mode check (first match)

1. User said retrofit / migrate docs / port `CONTEXT.md` → **Retrofit**. Open [retrofit.md](retrofit.md). Stop loading other mode files.
2. `docs/index.md` exists → **Maintain** (below). Do **not** open `retrofit.md` or `producer-profile.md`.
3. No `docs/index.md`, and any of `CONTEXT.md`, `docs/**/*.md`, or root `decisions.md` exist → **Retrofit** (same as 1). Filename glob only; no body reads to decide mode.
4. Else → **Init** (greenfield). Copy `templates/`; open `producer-profile.md` only when filling required frontmatter.
5. If 3 vs 4 is unclear → **ask** (init skeleton vs retrofit assessment).

**Not legacy alone:** `AGENTS.md`, `README.md`, `CLAUDE.md` (pointer-trim on Init applies to `AGENTS.md` / `CLAUDE.md` only — not root `README.md`).

**Explicit user wins:** `docs/index.md` + user says retrofit → Retrofit. Wrap-up with a bundle → Maintain event 6, never Retrofit.

---

Daily producer for the software-repo OKF profile. Detail and folder/type map: [producer-profile.md](producer-profile.md). Pair with `plan-build` for WIP trees.

**Authority:** code > `docs/` > agentmemory.

## When to use (Maintain)

- Any of the seven events below.
- Wrap-up ("hand off", "wrap up the session") — event 6.

## Query

Pick settled **or** WIP, not both.

1. Prefer `AGENTS.md` when present, else `README.md` → `docs/index.md`.
2. Filter by Settled / In progress, then folder, `type`, `status`.
3. Open 1–3 files. Stop.

Resume an effort: that effort’s `HANDOFF.md` first, then only its required reading.

## Init (greenfield)

Copy `templates/` to the repo root. Fill `{{PROJECT}}` / `{{ONE_LINE_PURPOSE}}`. Do not add `docs/decisions.md` or a plan tree until needed. Verify: `AGENTS.md` → `docs/index.md` → ≤3 files.

## Seven events

| #   | Event                                                             | Write                                                       |
| --- | ----------------------------------------------------------------- | ----------------------------------------------------------- |
| 1   | Decision or invariant locked                                      | `docs/decisions.md` (`DecisionLog`; `verified` when locked) |
| 2   | Ship / defer / priority change                                    | `docs/agents/` `ProductState`                               |
| 3   | Domain term now in code or issues                                 | `docs/concepts/` `Glossary`                                 |
| 4   | Ops path we actually run                                          | `docs/runbooks/`                                            |
| 5   | Durable agent obligation                                          | `docs/agents/` `AgentGuide`                                 |
| 6   | Wrap-up, open question, deferred or in-flight work                | current `docs/plans/<slug>/` (`plan-build`)                 |
| 7   | Architecture, dependency **policy**, or coding/ops pattern locked | `docs/concepts/` `Architecture` / `Module` / `Invariant`    |

## Routing

**Hit** → write there. **Stay put** if a file already exists. **Ask** before a new settled page with no hit. **WIP default:** other new files go `draft` in the current plan tree. Never invent a settled page.

## On-write (same pass)

1. Refresh the folder `index.md` (`title` + `description`).
2. Refresh `docs/index.md` if the top-level map changed.
3. Prepend `docs/log.md` (newest first).
4. If under `docs/plans/<slug>/`, also update that effort’s `log.md`, or `progress-log.md` when `log.md` is absent.

`AGENTS.md` stays a pointer — no architecture essay. `README.md` stays human-facing; do not trim it to a pointer stub. Do not commit unless asked.

## Lint

`docs/plans/**` is WIP; other default folders are settled. `type` must be in that folder’s allowed set. No `layer`. No default `docs/questions/`. Do not split `decisions.md` or a glossary monolith without UAT evidence.

## Settle without move

Path is identity. Write the settled file; link from the plan; deprecate the WIP copy only if it would still look current. Do not move files.

## Memory

Write the matching file first. If agentmemory is up, save a **path-only gist**, not a body paste. Missing MCP is fine. Pitfalls stay in memory until they hit twice, then a `Lesson`.
