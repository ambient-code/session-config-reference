---
name: review
description: Perform a thorough code review with emphasis on security, correctness, and maintainability. Analyzes code changes and produces a structured review with actionable findings.
allowed-tools: Read, Glob, Grep, Bash
---

# Code Review

Perform a structured code review with security-first prioritization.

## Process

1. Identify the scope: either staged changes (`git diff --cached`), a specific commit, or specified files
2. Read each changed file completely to understand context
3. Analyze changes against the review checklist below
4. Produce a structured report

## Review Checklist

### Security (Critical)

- [ ] No hardcoded secrets, tokens, or API keys
- [ ] Input validation on all external data
- [ ] No SQL injection, XSS, or command injection vectors
- [ ] Authentication checked before authorization
- [ ] Sensitive data not logged or exposed in errors

### Correctness (High)

- [ ] Logic handles edge cases (nil, empty, boundary values)
- [ ] Error paths are handled and tested
- [ ] No race conditions in concurrent code
- [ ] Resource cleanup (close files, connections, channels)

### Performance (Medium)

- [ ] No unnecessary allocations in hot paths
- [ ] Database queries are bounded (LIMIT, pagination)
- [ ] No N+1 query patterns
- [ ] Appropriate use of caching

### Maintainability (Standard)

- [ ] Clear naming that reveals intent
- [ ] Functions have a single responsibility
- [ ] No duplicated logic that should be extracted
- [ ] Adequate comments on non-obvious decisions

## Output Format

```markdown
## Code Review: [scope description]

### Summary
[1-2 sentence overview of the changes and overall assessment]

### Findings

| # | Severity | File:Line | Finding | Suggestion |
|---|----------|-----------|---------|------------|
| 1 | CRITICAL | path:42 | ... | ... |

### Positive Observations
- [Things done well worth acknowledging]

### Verdict
[APPROVE / REQUEST CHANGES / NEEDS DISCUSSION]
```

## Rules

- Always read the full file, not just the diff, to understand context
- Be specific: reference exact lines, not vague areas
- Distinguish between blocking issues and suggestions
- Acknowledge what is done well, not just problems
