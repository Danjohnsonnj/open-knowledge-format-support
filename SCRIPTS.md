# Scripts

Repository-level commands for installing and verifying the in-repo `okf-docs` skill.

## install-okf-docs

Install `skills/okf-docs/` to global skill roots.

```sh
./scripts/install-okf-docs --target auto --mode copy
./scripts/install-okf-docs --target both --mode link --replace
```

| Option | Values | Default |
| ------ | ------ | ------- |
| `--target` | `cursor`, `agents`, `both`, `auto` | `auto` |
| `--mode` | `copy`, `link` | `copy` |
| `--replace` | flag | off |

Destinations:

- Cursor: `~/.cursor/skills/okf-docs`
- Agents: `~/.agents/skills/okf-docs`

`auto` picks the sole existing install or sole existing skills parent. When both or neither apply, it prompts on an interactive terminal; otherwise pass `--target` explicitly.

## smoke-install-okf-docs

Run installer smoke checks under a temporary `HOME` (does not touch your real skill directories).

```sh
./scripts/smoke-install-okf-docs
```

Covers copy/link installs for cursor, agents, and both, plus the non-interactive `auto` failure path.
