# Adapters

## Adapter Responsibility

Adapters connect Reform's harness to a runtime.
They translate the core workflow into runtime-specific actions.

## Adapter Duties

- detect supported capabilities
- map harness intents to runtime calls
- normalize responses
- handle permissions, sessions, tools, and hooks
- degrade when capabilities are missing
- record runtime limits

## Adapter Limits

- do not define methodology
- do not decide task splits
- do not define acceptance criteria
- do not replace memory
- do not leak runtime semantics into the core protocol

## Compatibility Rule

The core recognizes capabilities, not brands.
