# Evidence

Evidence checkpoints make completion claims inspectable.
They are workflow requirements, not runtime logs.

## Checkpoints

Use these checkpoints for bounded work:

1. `intake` - record the requested end state, constraints, and known acceptance criteria.
2. `plan` - record the intended files, commands, runtime targets, and verification approach.
3. `change` - record the source diff or generated runtime files that changed.
4. `verify` - record command output, runtime output, screenshots, citations, or documented failure.
5. `handoff` - record remaining work, blockers, and resume instructions when the task does not finish.

## Evidence Fields

Each checkpoint should be understandable without replaying the whole session.

- `checkpoint` - one of the checkpoint names above
- `claim` - the specific claim being made
- `source` - file, command, runtime output, screenshot, citation, or failure reason
- `result` - passed, failed, unavailable, or deferred
- `next` - the next required action when the result is not passed

## Stop Rules

- Do not mark acceptance complete when evidence is missing or only implied.
- Do not use generated runtime files as the maintained source of truth.
- Do not hide unsupported runtime capabilities; record the degraded behavior.
- Do not rewrite Reform's human-facing decisions as if the agent authored them.

## Storage Rule

For now, evidence may live in the final response, TODO updates, adapter docs, or a small task note.
Add durable evidence storage only when repeated work shows the shape is stable.
