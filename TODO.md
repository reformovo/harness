# TODO

Goal:

> Reform's harness can be installed into multiple agent runtimes from one source repository.

This TODO tracks the first installable loop.
It does not cover full orchestration, memory, evidence checkpoints, or background agents yet.

Installability must follow each runtime's native extension path.
`scripts/install.py` was a prototype materializer and is not the acceptance path.

## 1. Define Source Contract

- [x] Add `harness.json` as the source manifest.
- [x] Include `name`, `description`, `version`, and `supported_runtimes`.
- [x] List installable resources: `roles`, `skills`, `configs`, optional `hooks`, and optional `plugins`.
- [x] Document that `harness.json` describes Reform's harness, not a runtime config.
- [x] Keep install, enable, authorize, and approve states separate for plugin-capable resources.
- [x] Keep the manifest small enough to read directly.

Acceptance:

- [x] A person can inspect `harness.json` and understand what the harness contains.
- [x] No runtime-specific paths are required in the source manifest.
- [x] Plugin-capable resources declare capabilities without depending on one runtime's plugin format.

## 2. Create Runtime Adapter Targets

- [x] Add `adapters/codex/README.md`.
- [x] Add `adapters/opencode/README.md`.
- [x] For each adapter, document the runtime-native install mapping:
  - source resource
  - runtime-native manifest, plugin entry, or config hook
  - runtime discovery path
- [x] For each adapter, document how plugin capabilities map to that runtime.
- [x] Keep adapters limited to installation concerns.
- [x] Do not put methodology, task splitting, or workflow rules inside adapters.

Acceptance:

- [x] Codex has a clear plugin install target using `.codex-plugin/plugin.json` and a repo-scoped Codex marketplace.
- [x] OpenCode has a clear native install target that generates project-scoped `.opencode/agents/` and `.opencode/skills/`; `opencode.json` plugin entries are reserved for future hook, tool, or MCP code.
- [x] The same source resources can be mapped into both runtimes without relying on the removed Python installer.

## 3. Prepare Minimal Installable Resources

- [x] Add `roles/orchestrator.md` as the first role definition.
- [x] Add one minimal skill or keep `skills/README.md` as the first skill index.
- [x] Add or validate the Codex plugin structure, likely `.codex-plugin/plugin.json` plus skills.
- [x] Validate the generated OpenCode native project structure for agents and skills; no package plugin is needed until the harness ships OpenCode hook, tool, or MCP code.
- [x] Use `docs/plugins.md` as the boundary for when a skill becomes a plugin bundle.
- [x] Keep all content specific to Reform's harness.

Acceptance:

- [x] Runtime-native install exposes at least one role or skill in Codex.
- [x] Runtime-native install exposes at least one role or skill in OpenCode.
- [x] Runtime-specific manifests are derived from or checked against one source contract, not maintained as unrelated duplicates.

## 4. Use Runtime-Native Installer Entry

- [x] Remove the prototype `scripts/install.py` path from the first installable loop.
- [x] Document Codex install through a Codex-native plugin flow.
- [x] Document OpenCode install through OpenCode-native project discovery.
- [x] Keep `harness.json` as the source contract, not the runtime installer.
- [x] If generation remains useful, keep it as a development sync/check step, not the user-facing install path.

Acceptance:

- [x] Codex install uses Codex plugin discovery, not the removed Python installer.
- [x] OpenCode install uses OpenCode runtime discovery, not the removed Python installer.
- [x] Failed installs or load failures identify whether the issue is manifest, plugin package/config, path/cache, or runtime discovery.

## 5. Verify Runtime Discovery

- [x] Document how to verify Codex discovers the installed harness after runtime-native install.
- [x] Document how to verify OpenCode discovers the installed harness after runtime-native install.
- [x] Record the expected plugin manifests, config entries, cache paths, or project-scoped discovery locations for both runtimes.
- [x] Record known unsupported runtime capabilities.

Acceptance:

- [x] Codex can see the installed `orchestrator` agent through runtime-native project agent discovery.
- [x] Codex can see the installed `skills-index` skill through runtime-native plugin discovery.
- [x] OpenCode can see the installed `orchestrator` agent through runtime-native project discovery.
- [x] OpenCode can see the installed `skills-index` skill through runtime-native project discovery.
- [x] Missing capabilities degrade explicitly instead of being hidden.

## Later

- [x] Add evidence checkpoints.
- [x] Add durable memory.
- [ ] Decide whether a development sync/check tool is still useful after runtime-native install is working.
- [ ] Add richer skills.
- [ ] Add more roles only when Reform actually uses them.
- [ ] Add background agent support after installability is stable.
- [ ] Extract a reusable `build-your-own-harness` path only after Reform's harness proves useful.
