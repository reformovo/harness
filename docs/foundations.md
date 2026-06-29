# Foundations

Model improvements can reduce prompt tricks and shallow role play.
They do not replace the parts of a harness that deal with external systems, long-lived state, permissions, scheduling, evidence, and portability.

## Runtime Boundary

A runtime owns execution.

Runtime responsibilities include:

- model calls
- built-in tools
- file and shell execution
- user interface
- session mechanics
- permission prompts
- runtime-native plugins, hooks, skills, MCP, and commands
- local or remote execution
- product authentication
- runtime-local logs and traces

The harness owns working style and portability.

Harness responsibilities include:

- Reform's workflow protocol
- cross-runtime capability model
- runtime adapter mappings
- durable roles, skills, playbooks, and memory rules
- evidence and acceptance standards
- extension boundaries
- scheduling, messaging, monitoring, and operational policy

If a concern is about how one product executes a task, it belongs near the runtime.
If a concern is about how Reform wants work to happen across products, it belongs in the harness.

## Non-Replaced Capabilities

Better models do not remove the need for:

- multi-agent responsibility separation
- parallel execution and result merging
- external message intake and push notifications
- scheduled tasks
- telemetry, monitoring, and audit logs
- permissions and safety boundaries
- durable memory and state
- evidence-based verification
- runtime adapters
- tool, plugin, MCP, and connector orchestration
- cost, latency, and model routing policy

These are harness concerns because they require state, systems, policy, or coordination outside a single model response.

## Core Foundations

### Source Contract

The source contract answers what the harness contains.

It should describe:

- roles
- skills
- workflows
- playbooks
- memory rules
- hooks
- plugins
- configs
- supported runtimes

This should stay small enough for a person to inspect directly.

### Capability Model

The capability model answers what a runtime can and cannot do.

Examples:

- file read and write
- shell execution
- browser use
- MCP
- hooks
- plugins
- parallel sessions
- background tasks
- external connectors
- approvals
- telemetry

The harness should reason over capabilities before brands.

### Runtime Adapters

Adapters answer how the same harness is installed into each runtime.

Examples:

- Codex maps to plugin manifests, skills, hooks, MCP config, and app connectors.
- opencode maps to config, local plugins, event hooks, custom tools, and npm packages.

Adapters translate.
They do not define methodology.

### Workflow Protocol

The workflow protocol answers how a request becomes completed work.

It covers:

- intake
- clarification
- planning
- execution
- verification
- evidence recording
- handoff or resume
- stop conditions

This is the harness's core working style.

### Evidence And Verification

Evidence answers what counts as done.

Evidence may include:

- tests
- diffs
- logs
- screenshots
- citations
- runtime discovery output
- failure reasons

Completion without evidence does not count.

### Memory And State

Memory answers what should persist beyond one session.

It may include:

- user preferences
- project decisions
- effective runtimes
- noisy capabilities
- useful workflows
- current task state
- cross-session continuation notes

Model context is not a durable state store.

### Extension System

The extension system answers how new capabilities enter the harness.

Use:

- `skill` for reusable instructions
- `hook` for lifecycle control
- `tool` for callable actions
- `MCP` for external context or actions
- `plugin` when several capabilities need to be bundled, installed, enabled, or distributed

See `plugins.md` for plugin boundaries.

### Operations Layer

The operations layer answers how the harness runs over time.

It includes:

- scheduled tasks
- external message intake and push
- queues
- retries
- telemetry
- audit logs
- cost tracking
- alerting
- permissions
- secret handling

This layer is least likely to be replaced by stronger models because it depends on external systems and durable control.

## Build Order

Build the foundations in this order:

1. Source contract
2. Capability model
3. Runtime adapters
4. Workflow protocol
5. Evidence and verification
6. Memory and state
7. Extension system
8. Operations layer

The first installable loop should prioritize the first four.
The later layers should grow from real use, not from speculative framework design.
