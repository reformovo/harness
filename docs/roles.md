# Roles

This repository starts with the smallest useful role set.

## Core Roles

- `orchestrator` - decides the workflow, breaks work into steps, and coordinates execution
- `explorer` - gathers context, reads code, and maps the terrain
- `fixer` - makes bounded changes inside an assigned scope
- `reviewer` - checks risk, regressions, and completeness
- `librarian` - looks up external documentation and reference material

## Role Rule

Roles are responsibilities, not identities.
If a runtime cannot support a distinct role, the work should degrade into the smallest safe sequential flow.
