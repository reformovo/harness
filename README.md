# Harness

> Reform's personal harness for one or more agent runtimes.

This is Reform's working repository.
It contains the runtime wiring, skills, workflows, and preferences behind Reform's harness.

The design source lives in the companion repository:

- [build-your-own-harness](https://github.com/reformovo/build-your-own-harness)

## What This Repository Is

- Reform's personal harness for one or more agent runtimes
- curated skills and workflows
- explicit responsibilities
- evidence-driven checkpoints
- reusable playbooks and preferences

## What This Repository Is Not

- a heavy abstraction layer
- a framework that hides how it works
- a one-size-fits-all opinionated product
- a dependency that forces every future user into the same workflow

## Start Here

1. Read `docs/vision.md`
2. Read `docs/workflows.md`
3. Read `docs/adapters.md`
4. Inspect the active runtime configuration
5. Use the smallest useful role set first

## Design Principle

Reform builds a harness that fits Reform.

## Repository Shape

- `adapters/` - runtime-specific execution adapters
- `roles/` - role definitions and prompts
- `skills/` - reusable workflow skills
- `memory/` - personal preferences and decision history
- `playbooks/` - repeatable task patterns
- `configs/` - runtime and adapter configuration
- `docs/` - project decisions and operating rules
