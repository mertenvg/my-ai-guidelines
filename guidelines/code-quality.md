# Code Quality Standards

---

## General Principles

- Functions should have a single responsibility.
- Prefer early returns to deep nesting.
- Avoid magic values; use named constants or enums.
- Use descriptive naming. Names should reveal intent.
- Comments explain **why**, not what. If the code needs a "what" comment, the code
  should be rewritten to be clearer.

---

## Defensive Programming

- Validate inputs at system boundaries (user input, external APIs, config).
- Trust internal code and framework guarantees — do not add redundant validation.
- Assume external systems can fail. Handle failure paths explicitly.
- Never silently ignore errors or discard return values.

---

## Naming Conventions

- Use the language's idiomatic naming style (e.g., `camelCase` in JS/TS,
  `snake_case` in Python, short descriptive names in Go).
- Method names should not repeat the type name when the package already provides
  context (e.g., `driver.Store.GetByID` not `GetDriverByID`).
- Exported/public identifiers require clear documentation.
- Keep names short but descriptive. Abbreviations are acceptable when conventional
  (e.g., `ctx`, `db`, `req`, `resp`).

---

## Error Messages

- Prefix error messages with the module or context they originate from.
- Include enough context to diagnose the issue without access to the source.
- Use consistent formatting: `"module: operation: %w"`.

```go
// Good
return fmt.Errorf("driver: get by id: %w", err)

// Bad
return fmt.Errorf("error: %w", err)
return err
```
