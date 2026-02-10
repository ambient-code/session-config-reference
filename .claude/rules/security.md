# Security Standards

These rules apply to ALL files in the workspace.

## Secret Handling

- NEVER hardcode secrets, API keys, tokens, or passwords in source code
- NEVER log sensitive values — use length or hash for debugging: `log.Printf("token len=%d", len(token))`
- Use environment variables or secret management systems for all credentials
- If you encounter a secret in code during review, flag it immediately

## Input Validation

- Validate and sanitize all external input before use
- Use parameterized queries for database operations — never string concatenation
- Validate URL inputs before making HTTP requests
- Check for path traversal in file operations: reject paths containing `..`

## Dependency Awareness

- Prefer well-maintained dependencies with active security response teams
- Check for known vulnerabilities before adding new dependencies
- Pin dependency versions in production configurations
- Do not use `curl | bash` or `wget | sh` installation patterns

## Authentication and Authorization

- Always verify authentication before processing requests
- Check authorization at the resource level, not just the route level
- Use constant-time comparison for token validation
- Set appropriate timeouts on authentication tokens

## Error Handling

- Never expose internal error details in user-facing responses
- Log detailed errors server-side with request context
- Return generic error messages to clients
- Do not include stack traces in production API responses
