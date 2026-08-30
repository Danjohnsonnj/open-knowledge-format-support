# open-knowledge-format-support

Canonical source for the **okf-docs** agent skill and the OKF v0.2 software-repo documentation profile as a practical way to keep agent-readable repo docs versioned, loadable without MCP, and colocated with your code.

## What this is

[Open Knowledge Format (OKF)](https://github.com/GoogleCloudPlatform/open-knowledge-format) defines a markdown + YAML frontmatter wiki pattern for LLM agents. This repository ships:

- **`skills/okf-docs/`** — the `okf-docs` skill (init, maintain, and retrofit OKF-compatible `docs/` bundles)
- **`docs/`** — a dogfood documentation bundle and design notes for the profile
- **Installer scripts** — deploy the skill to Cursor or agent skill roots

Code wins over wiki. `AGENTS.md` and `README.md` index; the bundle holds the knowledge.

## Quick start

Install the skill to your environment:

```sh
./scripts/install-okf-docs --target auto --mode copy
```

For local development against this repo, symlink instead:

```sh
./scripts/install-okf-docs --target both --mode link --replace
```

Verify the installer:

```sh
./scripts/smoke-install-okf-docs
```

See [SCRIPTS.md](SCRIPTS.md) for full options (`--target`, `--mode`, `--replace`).

## Install targets

| Target | Path                        |
| ------ | --------------------------- |
| Cursor | `~/.cursor/skills/okf-docs` |
| Agents | `~/.agents/skills/okf-docs` |

Edit the skill in **`skills/okf-docs/`** in this repository — not in your home directory. Re-run the installer after changes (or use `link` mode).

## Documentation

- [docs/index.md](docs/index.md) — bundle hub (settled knowledge and in-progress efforts)
- [skills/okf-docs/SKILL.md](skills/okf-docs/SKILL.md) — skill entry point
- [skills/okf-docs/producer-profile.md](skills/okf-docs/producer-profile.md) — implementer spec for the software-repo profile

## Repository layout

```
skills/okf-docs/     Canonical okf-docs skill source
docs/                OKF documentation bundle (concepts, runbooks, plans)
scripts/             install-okf-docs, smoke-install-okf-docs
SCRIPTS.md           Command reference
```
