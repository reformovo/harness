# Codex Adapter

This adapter maps Reform's source harness into Codex-discoverable files.
It only covers installation targets and capability translation.

## Install Target

The Codex target is a runtime-native plugin install.
Codex should discover Reform's harness through a Codex plugin manifest, not through a standalone repository copy script.

| Source resource | Runtime-native artifact | Runtime discovery path |
| --- | --- | --- |
| `harness.json` | source contract checked by the adapter | adapter input, not a Codex config |
| `roles/*.md` | generated `.codex/agents/<id>.toml` custom agent file | project-scoped Codex agent discovery |
| `skills/**/SKILL.md` or `skills/README.md` | `plugins/harness/skills/<id>/SKILL.md` referenced by `.codex-plugin/plugin.json` | Codex plugin skill discovery |
| `configs/` | Codex config fragments when needed | Codex config or plugin manifest |
| optional `hooks/` | plugin hook files when a hook exists | Codex plugin bundle |
| optional `plugins/` | `plugins/harness/.codex-plugin/plugin.json` plus plugin package contents | Codex plugin install flow |
| repo plugin catalog | `.agents/plugins/marketplace.json` | `codex plugin marketplace add <repo-root>` then `codex plugin add harness@reform` |

## Verified Install Method

From a checkout of this repository, install the repo marketplace and then install the plugin:

```bash
codex plugin marketplace add <repo-root>
codex plugin add harness@reform
codex plugin list --json
codex debug prompt-input "probe"
codex exec --ephemeral --sandbox read-only "Verify whether the project-scoped custom agent named orchestrator can be spawned..."
```

For isolated verification, set `CODEX_HOME` to a temporary directory before each `codex plugin` and `codex debug` command.
This was verified on 2026-06-29 with `CODEX_HOME=/private/tmp/harness-reform-codex-home` and `<repo-root>=/Users/kaikai/projects/harness`.

The `.codex/agents/orchestrator.toml` file used by the final command is runtime-local install output.
It is ignored by Git and should be created by the install/bootstrap step from `roles/orchestrator.md`, not maintained as source.

Expected evidence:

- `codex plugin list --json` reports `harness@reform` as installed and enabled.
- `codex debug prompt-input "probe"` includes `harness:skills-index` from the plugin cache.
- `codex exec --ephemeral --sandbox read-only ...` can spawn the project-scoped `orchestrator` agent and returns `ORCHESTRATOR_AGENT_DISCOVERED`.

## Plugin Capability Mapping

Codex receives plugin-capable resources through Codex plugin bundles.
The adapter translates portable capabilities from `harness.json`; it does not infer capabilities from file names.

| Harness capability | Codex mapping |
| --- | --- |
| `skills` | bundled Codex skill files referenced by the plugin manifest |
| `hooks` | Codex plugin hooks when the runtime supports the lifecycle point |
| `tools` | Codex plugin tools with explicit schemas |
| `mcp` | Codex MCP configuration generated from the plugin bundle |
| `apps` | Codex app or connector setup that still requires separate authorization |
| `assets` | plugin assets copied into the plugin bundle |

Install, enable, authorize, and approve remain separate states.
Installing a Codex plugin makes it discoverable, but external app authorization and trust-sensitive approvals remain runtime-owned.

## Discovery Verification

After installing through the Codex plugin flow, verify runtime discovery with runtime commands.
Plugin files or generated artifacts in expected paths are not sufficient evidence.

| Resource | Discovery command | Expected evidence | Status |
| --- | --- | --- | --- |
| `harness` plugin | `codex plugin list --available --json` after adding the repo marketplace | Output includes `harness@reform` with source `plugins/harness`. | Verified 2026-06-29 |
| `skills-index` skill | `codex debug prompt-input "probe"` after installing the plugin | Output includes `harness:skills-index` from the plugin cache. | Verified 2026-06-29 |
| `orchestrator` agent | `codex exec --ephemeral --sandbox read-only "Verify whether the project-scoped custom agent named orchestrator can be spawned..."` | Output includes `ORCHESTRATOR_AGENT_DISCOVERED` after spawning the project-scoped `orchestrator` agent. | Verified 2026-06-29 |

Codex agent discovery uses project-scoped custom agent files.
It is separate from Codex plugin skill discovery.

Expected runtime-native install artifacts:

- `.codex-plugin/plugin.json`
- plugin skills referenced by the manifest
- `.agents/plugins/marketplace.json`
- `plugins/harness/` referenced by `.agents/plugins/marketplace.json`
- generated `.codex/agents/orchestrator.toml` for the custom agent path described in Codex subagent documentation

Tracked source artifacts:

- `harness.json`
- `roles/orchestrator.md`
- `skills/README.md`
- `.agents/plugins/marketplace.json`
- `plugins/harness/.codex-plugin/plugin.json`
- `plugins/harness/skills/skills-index/SKILL.md`

Ignored install artifacts:

- `.codex/agents/orchestrator.toml`
- any Codex plugin cache, state, logs, or user-specific config

## Unsupported Or Degraded Capabilities

- Codex agent discovery is not a plugin capability in this first loop; it uses `.codex/agents/`.
- There is no current source hook, tool, MCP, app, or asset bundle to install.
- Plugin install does not imply enablement, external app authorization, or trust-sensitive approval.
- Runtime discovery cannot be proven from files alone; it must be confirmed in Codex after install.

## Failure Boundaries

- Manifest failure: `python3 -m json.tool harness.json` or plugin manifest JSON parsing fails.
- Plugin package failure: `codex plugin add harness@reform --json` fails after the marketplace is added.
- Path or cache failure: install succeeds but the reported `installedPath` is missing or points outside the expected Codex cache.
- Runtime discovery failure: install succeeds but `codex debug prompt-input` does not include `harness:skills-index`.

## Adapter Limits

This adapter does not define methodology, task splitting, workflow rules, or acceptance criteria.
Those remain harness concerns.
