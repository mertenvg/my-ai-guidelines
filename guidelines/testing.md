# Testing Standards

---

## When to Write Tests

AI must add or update tests when:

- Behavior changes or new behavior is introduced.
- A bug is fixed (add a regression test).
- Security-sensitive logic is modified.

---

## What to Test

Tests should cover:

- Core business logic and happy paths.
- Edge cases and boundary conditions.
- Error paths and failure modes.
- Security-sensitive logic (auth, validation, access control).

---

## Testing Principles

- **Test behavior, not implementation details.** Tests should verify observable
  outcomes, not internal state or method call counts.
- **Tests must be deterministic.** No flaky tests. No reliance on real
  network, time, or external services in unit tests.
- **Prefer table-driven tests** for testing multiple input/output permutations.
  This reduces duplication and makes it easy to add new cases.
- **Use fakes and stubs over mocks** when possible. Fakes provide more realistic
  behavior and are less brittle than mock-based assertions.

---

## Test Organization

- Place tests in the same package as the code they test (`_test.go` suffix in Go).
- Name tests clearly: `TestThing_Scenario_Expectation`.
- Keep test setup minimal — extract common setup into helpers only when shared
  across multiple test functions.

---

## Assertions (Go)

- Use `require` for preconditions and error checks — these abort the test on
  failure, preventing cascading nil-pointer panics.
- Use `assert` for value checks — these record failures but let the test continue,
  giving you all failures in one run.

```go
// require for errors (abort early)
require.NoError(t, err)
require.NotNil(t, result)

// assert for values (continue on failure)
assert.Equal(t, expected, result.Name)
assert.True(t, result.Active)
```

---

## Integration Tests

- Integration tests may use real databases, network, or external services.
- Use appropriate timeouts (e.g., 120s for tests that spin up real nodes).
- Clearly separate integration tests from unit tests via build tags or naming
  conventions.
- Run unit tests by default; integration tests on explicit request.

---

## Verification Before Committing

Always verify locally before committing:

```bash
# Go
go test ./...
go vet ./...

# TypeScript
npm run lint
npm run build
npm test
```
