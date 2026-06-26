# Adapters

## Adapter Responsibility

Adapters connect the harness to a specific runtime.
They translate the core workflow into runtime-specific actions.

## Adapter Duties

- detect supported capabilities
- map harness intents to runtime-specific calls
- normalize runtime responses into a common shape
- handle permissions, sessions, tools, and hooks
- degrade gracefully when capabilities are missing
- record runtime-level errors and limits

## Adapter Limits

- do not define methodology
- do not decide how tasks are split
- do not define acceptance criteria
- do not replace the memory layer
- do not leak runtime-specific semantics into the core protocol

## Compatibility Rule

The core only recognizes capabilities, not brands.
If a runtime exposes the same capability, it can attach to the same harness.
