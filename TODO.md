# TODO

Goal:

> Reform's harness can be installed into multiple agent runtimes from one source repository.

This TODO tracks the first installable loop.
It does not cover full orchestration, memory, evidence checkpoints, or background agents yet.

## 1. Define Source Contract

- [ ] Add `harness.json` as the source manifest.
- [ ] Include `name`, `description`, `version`, and `supported_runtimes`.
- [ ] List installable resources: `roles`, `skills`, `configs`, optional `hooks`, and optional `plugins`.
- [ ] Document that `harness.json` describes Reform's harness, not a runtime config.
- [ ] Keep install, enable, authorize, and approve states separate for plugin-capable resources.
- [ ] Keep the manifest small enough to read directly.

Acceptance:

- [ ] A person can inspect `harness.json` and understand what the harness contains.
- [ ] No runtime-specific paths are required in the source manifest.
- [ ] Plugin-capable resources declare capabilities without depending on one runtime's plugin format.

## 2. Create Runtime Adapter Targets

- [ ] Add `adapters/codex/README.md`.
- [ ] Add `adapters/opencode/README.md`.
- [ ] For each adapter, document the install mapping:
  - source resource
  - generated or copied runtime file
  - runtime discovery path
- [ ] For each adapter, document how plugin capabilities map to that runtime.
- [ ] Keep adapters limited to installation concerns.
- [ ] Do not put methodology, task splitting, or workflow rules inside adapters.

Acceptance:

- [ ] Codex and OpenCode each have a clear install target.
- [ ] The same source resources can be mapped into both runtimes.

## 3. Prepare Minimal Installable Resources

- [ ] Add `roles/orchestrator.md` as the first role definition.
- [ ] Add one minimal skill or keep `skills/README.md` as the first skill index.
- [ ] Decide the Codex generated structure, likely `.codex-plugin/plugin.json` plus skills.
- [ ] Decide the OpenCode generated structure, likely `.opencode` config/plugin resources.
- [ ] Use `docs/plugins.md` as the boundary for when a skill becomes a plugin bundle.
- [ ] Keep all content specific to Reform's harness.

Acceptance:

- [ ] The install output contains at least one role or skill.
- [ ] Runtime-specific files are generated or copied from one source, not maintained as unrelated duplicates.

## 4. Add Installer Entry

- [ ] Add a minimal install command or documented script entry.
- [ ] Support `install codex`.
- [ ] Support `install opencode`.
- [ ] Installer behavior:
  - read `harness.json`
  - select the runtime adapter
  - copy or generate runtime files
  - print install result and verification steps
- [ ] Keep the installer boring and inspectable.

Acceptance:

- [ ] `install codex` produces Codex-discoverable harness files.
- [ ] `install opencode` produces OpenCode-discoverable harness files.
- [ ] Failed installs identify whether the issue is manifest, adapter, path, or runtime discovery.

## 5. Verify Runtime Discovery

- [ ] Document how to verify Codex discovers the installed harness.
- [ ] Document how to verify OpenCode discovers the installed harness.
- [ ] Record the expected install locations for both runtimes.
- [ ] Record known unsupported runtime capabilities.

Acceptance:

- [ ] Codex can see the installed resource.
- [ ] OpenCode can see the installed resource.
- [ ] Missing capabilities degrade explicitly instead of being hidden.

## Later

- [ ] Add evidence checkpoints.
- [ ] Add durable memory.
- [ ] Add richer skills.
- [ ] Add more roles only when Reform actually uses them.
- [ ] Add background agent support after installability is stable.
- [ ] Extract a reusable `build-your-own-harness` path only after Reform's harness proves useful.
