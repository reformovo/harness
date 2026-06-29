# Harness Agent Contract

## Project Shape

This repository is Reform's personal harness for agent runtimes. It is currently a documentation-first source contract for roles, skills, workflows, memory, runtime adapters, playbooks, and configs.

## Directory Map

- `docs/` - project decisions, foundations, workflows, adapter rules, and operating docs
- `adapters/` - runtime-specific execution adapter definitions
- `configs/` - runtime and adapter configuration
- `roles/` - role definitions and prompts
- `skills/` - reusable workflow skills
- `memory/` - Reform's preferences and prior decisions
- `playbooks/` - repeatable task patterns
- `.agents/skills/` - local agent skills used to maintain this repository

## Must Always

- Keep the harness explicit and inspectable; prefer small Markdown/source-contract changes over speculative framework code.
- Preserve the boundary from `docs/foundations.md`: runtimes own execution, the harness owns working style and portability.
- Tie every completion claim to evidence: diff, command output, test result, screenshot, citation, or documented failure.
- Declare the intended edit file list before changing files. Target no more than 5 files and 200 changed lines per task unless scope is explicitly expanded.
- Update this file in the same change when project commands, directory responsibilities, or agent rules change.
- For docs, keep headings and lists consistent with the surrounding file style.

## Must Never

- Do not turn this repository into a heavy abstraction layer or one-size-fits-all framework.
- Do not add runtime-specific behavior outside the relevant adapter/config boundary.
- Do not claim verification passed without running the stated command or clearly marking it unavailable.
- Do not commit secrets, `.env` files, tokens, local credentials, or private runtime logs.
- Do not rewrite human-facing explanations, issue text, PR descriptions, or personal memory as if the agent were the author.

## Boundaries

- Always: read the nearest relevant README or doc before changing a directory.
- Ask first: installing dependencies, adding a package manager, introducing executable code, changing repository layout, or deleting files.
- Never: force-push, reset user work, disable verification to finish faster, or edit unrelated files.

## Commands

- List tracked project files: `rg --files`
- Inspect worktree status: `git status --short`
- Check patch whitespace: `git diff --check`

There is no package-level lint, type-check, test, or build command yet. When executable code is added, add the real commands here in the same change and run them before declaring completion.

## Definition of Done

- Intended files were declared before editing, or scope expansion was explicitly justified.
- Relevant docs were read before changing their area.
- `git diff --check` passes for changed files.
- Any unavailable verification is called out with the reason.
- The final diff is small enough to explain line by line.

## Skills

- Vibe coding workflow, AI coding constraints, scope lock, verification gates, or contract maintenance -> use `.agents/skills/reform/SKILL.md`.
