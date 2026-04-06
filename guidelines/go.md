# Go Guidelines

---

## Formatting and Tooling

Code must conform to:

- `gofmt` — mandatory, no exceptions.
- `go vet` — mandatory before committing.
- Repository linters (e.g., `golangci-lint`) if present.

Import groups should be ordered: standard library, third-party, then local packages.

---

## Error Handling

- Always return errors with context using `fmt.Errorf("context: %w", err)`.
- Wrap errors with `%w` when the caller may need to inspect the underlying error.
- Do not panic for expected runtime failures — return an error.
- Panic only for programmer errors or impossible states (e.g., failed prepared
  statement initialization).
- Use sentinel errors for common conditions. Check with `errors.Is()` or
  `errors.As()`.

---

## Design

- Prefer concrete types over interfaces for internal code.
- Define interfaces at the consumption boundary, not alongside the implementation.
- Keep interfaces small — one to three methods.
- Avoid global mutable state. Use dependency injection via constructor functions.
- Exported identifiers require GoDoc-friendly comments.

---

## Concurrency

- Use `context.Context` for all request lifecycles. Propagate cancellation.
- Prevent goroutine leaks — every goroutine must have a clear shutdown path.
- Bound concurrency — use worker pools or semaphores.
- Guard shared state with channels or mutexes.
- Code must be race-detector safe (`go test -race`).

---

## Handler Pattern

Use constructor functions that return handlers with injected dependencies:

```go
func NewGetHandler(db *sqlx.DB, auth *tokenator.Tokenator) gin.HandlerFunc {
    // prepare statements, set up dependencies
    return func(c *gin.Context) {
        // handle request
    }
}
```

Never use package-level variables for handler dependencies.

---

## Naming

- Follow Go naming conventions: short, descriptive names.
- Method names should not repeat the type or package name.
- Unexported types and constants should use concise, contextual names.
- Prefix SQL query constants with `q`: `qInsertUser`, `qGetByID`.
- Prefix unexported param structs with their purpose: `idParams`, `filterParams`.
