# OpenCode Adapter

This adapter maps Reform's source harness into OpenCode-discoverable files.
It only covers installation targets and capability translation.

## Install Target

The OpenCode target is a runtime-native project install.
OpenCode should discover Reform's harness through project-scoped agent and skill paths, not through a standalone repository copy script.

| Source resource | Runtime-native artifact | Runtime discovery path |
| --- | --- | --- |
| `harness.json` | source contract checked by the adapter | adapter input, not an OpenCode config |
| `roles/*.md` | generated `.opencode/agents/<id>.md` | OpenCode project agent discovery |
| `skills/**/SKILL.md` or `skills/README.md` | generated `.opencode/skills/<id>/SKILL.md` | OpenCode project skill discovery |
| `configs/` | `opencode.json` plugin entry or config fragments when a plugin capability exists | `opencode.json`, `.opencode/` |
| optional `hooks/` | OpenCode plugin hooks | configured plugin package |
| optional `plugins/` | OpenCode plugin package or local plugin entry when hooks, tools, or MCP need plugin code | `opencode.json` plugin array |

## Verified Install Method

This flow was verified on 2026-06-29 from the repository root:

```bash
opencode agent list
opencode debug agent orchestrator
opencode debug skill
```

The `.opencode/agents/orchestrator.md` and `.opencode/skills/skills-index/SKILL.md` files used by these commands are runtime-local install output.
They are ignored by Git and should be created by the install/bootstrap step from `roles/orchestrator.md` and `skills/README.md`, not maintained as source.

Expected evidence:

- `opencode agent list` includes `orchestrator (primary)`.
- `opencode debug agent orchestrator` includes `"name": "orchestrator"` and the prompt from `.opencode/agents/orchestrator.md`.
- `opencode debug skill` includes `"name": "skills-index"` and `.opencode/skills/skills-index/SKILL.md`.

No `opencode.json` plugin entry is required for the first loop because the verified resources are project-scoped agent and skill files.

## Plugin Capability Mapping

OpenCode receives plugin-capable resources through local plugins, configured plugin packages, and runtime-native resource directories.
The first loop uses runtime-native directories for the role and skill because no hook, tool, or MCP code exists yet.
The adapter translates portable capabilities from `harness.json`; it does not infer capabilities from file names.

| Harness capability | OpenCode mapping |
| --- | --- |
| `skills` | project skill directories in this first loop; plugin-registered skill resources when a package plugin exists |
| `hooks` | OpenCode plugin event hooks |
| `tools` | OpenCode plugin tools with explicit schemas |
| `mcp` | MCP configuration generated into OpenCode config |
| `apps` | external service setup that still requires separate authorization |
| `assets` | plugin-adjacent assets copied with the generated plugin |

Install, enable, authorize, and approve remain separate states.
Installing an OpenCode plugin makes it discoverable, but external service authorization and trust-sensitive approvals remain runtime-owned.

## Discovery Verification

After installing through the OpenCode project flow, verify runtime discovery with runtime commands.
Plugin files, config entries, or generated artifacts in expected paths are not sufficient evidence.

| Resource | Discovery command | Expected evidence | Status |
| --- | --- | --- | --- |
| `orchestrator` agent | `opencode agent list` | Output includes `orchestrator (primary)` from project discovery. | Verified 2026-06-29 |
| `orchestrator` agent details | `opencode debug agent orchestrator` | Output includes `"name": "orchestrator"` and the role prompt from `.opencode/agents/orchestrator.md`. | Verified 2026-06-29 |
| `skills-index` skill | `opencode debug skill` | Output includes `"name": "skills-index"` and `.opencode/skills/skills-index/SKILL.md`. | Verified 2026-06-29 |

Expected runtime-native install artifacts:

- generated `.opencode/agents/orchestrator.md`
- generated `.opencode/skills/skills-index/SKILL.md`
- `opencode.json` with a `plugin` entry only when a future hook, tool, MCP server, or package plugin exists
- any runtime cache path used by OpenCode's plugin manager when plugins are introduced

Tracked source artifacts:

- `harness.json`
- `roles/orchestrator.md`
- `skills/README.md`

Ignored install artifacts:

- `.opencode/agents/orchestrator.md`
- `.opencode/skills/skills-index/SKILL.md`
- any OpenCode package install, cache, state, logs, or user-specific config

## Unsupported Or Degraded Capabilities

- There is no current source hook, tool, MCP, app, or asset bundle to install.
- Plugin install does not imply enablement, external service authorization, or trust-sensitive approval.
- Runtime discovery cannot be proven from files alone; it must be confirmed in OpenCode after install.

## Failure Boundaries

- Manifest failure: `python3 -m json.tool harness.json` fails or the source item path is missing.
- Project config failure: OpenCode refuses project config or project-scoped resource files.
- Path failure: `.opencode/agents/orchestrator.md` or `.opencode/skills/skills-index/SKILL.md` is missing from the project root.
- Runtime discovery failure: `opencode agent list`, `opencode debug agent orchestrator`, or `opencode debug skill` does not show the expected resource.

## Adapter Limits

This adapter does not define methodology, task splitting, workflow rules, or acceptance criteria.
Those remain harness concerns.
