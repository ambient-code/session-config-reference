---
name: review
description: Perform a code review on the current changes. Analyzes staged and unstaged diffs for bugs, security issues, and style violations.
allowed-tools: Read, Glob, Grep, Bash
---

# Code Review Skill

Review the current working tree for issues.

## Steps

1. Run `git diff` to see unstaged changes and `git diff --cached` for staged changes.
2. For each changed file, read the full file to understand context.
3. Check for:
   - Bugs or logic errors
   - Security vulnerabilities (injection, credential leaks, missing validation)
   - Style violations (inconsistent naming, overly complex functions)
   - Missing error handling
4. Summarize findings as a numbered list, grouped by severity:
   - **Critical**: Bugs or security issues that must be fixed
   - **Warning**: Code smells or potential problems
   - **Suggestion**: Style or readability improvements
5. If no issues are found, confirm the changes look good.
