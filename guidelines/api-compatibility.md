# API and Compatibility

---

## Backward Compatibility

- Maintain backward compatibility by default.
- Do not remove or rename public API fields, endpoints, or parameters without
  explicit instruction.
- Preserve public interfaces unless instructed otherwise.
- If a breaking change is necessary, document it explicitly with migration steps.

---

## API Design

- Validate request and response contracts at the boundary.
- Use versioned API paths (e.g., `/api/v1/`) to allow evolution.
- Return structured error responses with consistent format.
- Use appropriate HTTP status codes.

---

## Contract Evolution

- Additive changes (new fields, new endpoints) are safe.
- Removals, renames, and type changes are breaking — require a version bump.
- Document all breaking changes in release notes or changelogs.
