# Plugins

Plugins are optional extension bundles for Reform's harness.
They are useful when a workflow needs to travel as a package, not when a small local skill is enough.

## When to Use a Plugin

Use a plugin when an extension needs to bundle more than instructions:

- reusable skills
- runtime hooks
- external tool or MCP configuration
- app or connector setup
- assets or metadata for discovery
- install and enable state

Keep a workflow as a local skill when it only needs task instructions.

## Plugin Shape

A plugin should be a directory with a small manifest and optional bundled parts.

```text
my-plugin/
  plugin.json
  skills/
  hooks/
  tools/
  mcp.json
  assets/
```

For this harness, the manifest should do three jobs:

- identify the plugin
- declare the bundled capabilities
- describe how the plugin is installed, enabled, and trusted

The core harness should read capabilities from the manifest.
It should not infer behavior from runtime-specific filenames.

## Capability Types

Plugins may provide:

- `skills` - reusable workflow instructions
- `hooks` - lifecycle checks around sessions, tools, files, permissions, or compaction
- `tools` - callable runtime tools with explicit schemas
- `mcp` - external context or action servers
- `apps` - external services that require user authorization
- `assets` - icons, examples, screenshots, or other presentation files

Each capability must have a clear owner, trust boundary, and degradation path.

## Loading Rules

Plugin loading should be deterministic.

Recommended precedence:

1. managed or admin policy
2. repo-scoped marketplace or catalog
3. project-local plugins
4. personal plugins
5. runtime-curated plugins

When two plugins expose the same capability name, the resolver must report the conflict.
Silent override is only acceptable when the precedence rule is documented and visible.

## Trust Rules

Installing a plugin makes capabilities discoverable.
It must not automatically grant every capability full trust.

Trust-sensitive capabilities include:

- shell execution
- file reads and writes
- secret or environment access
- external app access
- MCP servers
- lifecycle hooks that can block or mutate tool calls

The harness should keep install, enable, authorize, and approve as separate states.

## Hook Guidance

Hooks are most valuable at boundaries:

- before and after tool execution
- when permissions are requested or answered
- when files are edited
- when commands finish
- when sessions become idle, error, or compact
- when shell environment is built

Hooks should record evidence or enforce a policy.
They should not hide workflow decisions inside runtime glue.

## Tool Guidance

Plugin tools need explicit schemas and short descriptions.
The harness should treat tools as capabilities, not as privileged shortcuts.

If a plugin tool has the same name as a built-in tool, the adapter must either reject it or expose the override explicitly.

## Compaction Guidance

Compaction hooks are useful for harness continuity.
They can inject task status, decisions, active files, blockers, and next steps into the continuation context.

A plugin may replace a compaction prompt only when that replacement is the point of the plugin.
Otherwise it should append structured context.

## Marketplace Guidance

A marketplace is a catalog of plugins.
For this harness, a catalog should be a plain data file that can be repo-scoped, personal, or managed.

Each catalog entry should include:

- stable plugin id
- display name
- source location
- version or revision
- capability summary
- trust-sensitive capabilities
- owner or publisher
- enable default

A single catalog can start with one plugin and grow into a curated list.
Do not require one catalog per plugin.

## Adapter Rule

Adapters translate plugin capabilities into runtime-specific mechanisms.
They do not define the plugin model.

Examples:

- a Codex adapter may map a plugin bundle to Codex plugin manifests, skills, MCP config, and hooks
- an opencode adapter may map a plugin to local plugin files, npm packages, event hooks, and custom tools

The core should stay portable.

## References

- OpenAI Codex plugins: https://developers.openai.com/codex/plugins
- OpenAI Codex build plugins: https://developers.openai.com/codex/plugins/build
- opencode plugins: https://opencode.ai/docs/plugins/
