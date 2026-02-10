# Session Configuration

This workspace is configured by the Ambient Code Platform session-config system.

## General Guidelines

- Write clean, readable code with meaningful variable names
- Follow the principle of least surprise
- Prefer composition over inheritance
- Keep functions under 50 lines where practical
- Every public function should have a clear docstring or comment explaining its purpose
- Handle errors explicitly — never silently swallow exceptions

## Commit Standards

- Use conventional commit format: `type(scope): description`
- Types: feat, fix, refactor, test, docs, chore, ci, perf
- Keep commits atomic — one logical change per commit
- Write commit messages that explain WHY, not just WHAT

## Code Review Priorities

When reviewing code, prioritize in this order:

1. Security vulnerabilities (injection, auth bypass, secret exposure)
2. Correctness (logic errors, edge cases, race conditions)
3. Performance (unnecessary allocations, N+1 queries, missing indexes)
4. Maintainability (naming, structure, documentation)
5. Style (formatting, conventions)

## Working with ACP Workspaces

- Artifacts should be written to the `artifacts/` directory
- Repository code lives under `repos/`
- Workflow definitions are in `workflows/`
- File uploads from the user are in `file-uploads/`
