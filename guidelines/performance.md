# Performance and Reliability

---

## Avoid

- **Unbounded concurrency** — always limit the number of concurrent goroutines,
  threads, or async operations.
- **Infinite retries** — use bounded retries with backoff and circuit breakers.
- **N+1 queries** — batch or join database queries instead of querying in a loop.
- **Unbounded memory growth** — use streaming, pagination, or bounded buffers for
  large data sets.

---

## Prefer

- **Bounded workers** — use worker pools with configurable concurrency limits.
- **Timeouts for all network calls** — never make a network call without a timeout
  or context deadline.
- **Cancellation-aware execution** — propagate `context.Context` and respect
  cancellation signals.
- **Predictable resource usage** — memory and CPU usage should be proportional to
  input size, not unbounded.

---

## Database

- Use connection pooling with sensible limits.
- Prepare statements once at startup, not per-request.
- Use pagination for list queries — never return unbounded result sets.
- Use `COALESCE` for partial updates instead of dynamic query building.
