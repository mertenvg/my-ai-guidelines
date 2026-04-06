# Security Requirements

These rules are **non-negotiable**. Security violations must be flagged and fixed
immediately, even if they exist in surrounding code.

---

## AI Must NEVER

- Log secrets, credentials, tokens, passwords, or private keys.
- Expose sensitive data in error messages, stack traces, or API responses.
- Construct SQL via string concatenation or interpolation.
- Introduce unsafe deserialization or `eval`-style execution.
- Disable or weaken TLS verification.
- Commit secrets, credentials, or private keys to version control.

---

## AI Must ALWAYS

- Validate and sanitize all user input at system boundaries.
- Prefer allow-lists over deny-lists for input validation.
- Ensure authorization checks are explicit on every protected route or endpoint.
- Use standard, well-vetted cryptographic libraries only — never roll custom crypto.
- Use parameterized queries or prepared statements for all database access.
- Apply the principle of least privilege for permissions and access scopes.

---

## Authentication and Authorization

- Authorization checks must be explicit — never rely on implicit trust.
- Use role-based or claim-based access control with middleware enforcement.
- Token validation must occur on every request to a protected resource.
- Session tokens and credentials must be stored securely (httpOnly cookies,
  encrypted storage — never localStorage for sensitive tokens).

---

## Data Protection

- Sensitive data must be encrypted at rest and in transit.
- PII and credentials must not appear in logs, metrics, or telemetry.
- Apply data minimization — do not collect or store more than needed.
