# Observability

---

## Logging

- Use structured logging with key-value pairs, not string concatenation.
- Include actionable context: service name, operation, identifiers.
- Use appropriate log levels:
  - **Error** — failures requiring attention.
  - **Warning** — degraded behavior that does not block the operation.
  - **Info** — significant operational events (startup, shutdown, config loaded).
  - **Debug** — protocol-level detail, request/response traces.
- Create component-scoped loggers when available (e.g., `log.With("component", "relay")`).
- Flush pending log messages before process exit.

---

## What Must NOT Appear in Logs

- Secrets, credentials, tokens, or private keys.
- Passwords or password hashes.
- PII beyond what is necessary for debugging.
- Full request/response bodies containing sensitive data.

---

## Error Context

- Errors should carry enough context to diagnose without access to the source code.
- Wrap errors with the operation and module: `"module: operation: %w"`.
- Use sentinel errors for common conditions and check with `errors.Is()`.
- Include relevant identifiers (user ID, request ID) in log entries, not in the
  error message itself.

---

## Telemetry

- Preserve existing telemetry and observability patterns in the project.
- Do not remove or disable metrics, tracing, or health check endpoints.
- Health check endpoints should be lightweight and not depend on external services.
