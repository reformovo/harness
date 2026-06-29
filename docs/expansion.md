# Expansion

This repository should stay understandable.

## How to Extend

- keep the core protocol stable
- add adapters behind the capability contract
- keep role count small
- package multi-part extensions as plugins only when a skill is too small
- prefer explicit evidence over implicit completion
- document any extension that changes workflow meaning

## Plugin-Level Extension

Use `plugins.md` when an extension needs bundled skills, hooks, tools, MCP config, app connectors, assets, or install metadata.
The core harness should recognize declared capabilities, while adapters map those capabilities to each runtime.

## Build Your Own Harness Principle

This repository is a practical instance of the method defined in `build-your-own-harness`.
Other people can fork it or reshape it to fit their own workflow.
