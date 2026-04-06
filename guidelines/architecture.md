# Architecture and Package Structure

---

## Module-Based Layout (MANDATORY)

**Use module-based (domain-driven) package structure, not classification-based.**

Every feature domain gets its own package containing everything it needs: types,
storage, logic, and errors. Do **not** group code by technical classification
(e.g., `models/`, `handlers/`, `controllers/`, `repositories/`).

### Why

Classification-based layouts (all models together, all handlers together) create
artificial coupling between unrelated domains and make it difficult to understand
or modify a single feature in isolation. Module-based layouts keep related code
together, making features self-contained and independently understandable.

### Correct (module-based)

```
cmd/<service>/internal/
  driver/
    model.go        # domain types, sentinel errors
    store.go        # data access, SQL, prepared statements
    handler.go      # HTTP/gRPC handlers (if applicable)
    handler_test.go
  booking/
    model.go
    store.go
    handler.go
  service/
    service.go      # orchestration layer, inter-module interfaces
```

### Incorrect (classification-based)

```
# DO NOT use this structure
models/
  driver.go
  booking.go
handlers/
  driver.go
  booking.go
repositories/
  driver.go
  booking.go
```

---

## Dependency Injection

- Inject dependencies via constructor functions. Never use package-level globals
  for mutable state.
- Constructor functions should accept interfaces, not concrete types, for
  dependencies that cross module boundaries.

```go
func NewService(drivers driverStore, documents documentStore) *Service {
    return &Service{drivers: drivers, documents: documents}
}
```

---

## Interface Design

- Define interfaces at the consumption boundary, not alongside the implementation.
- Keep interfaces small and focused — prefer single-method interfaces where
  practical.
- Use one unexported interface per dependency, not a single monolithic interface.

```go
// Good — defined where consumed, small, unexported
type driverStore interface {
    GetByID(ctx context.Context, id string) (*driver.Driver, error)
    Create(ctx context.Context, d *driver.Driver) (*driver.Driver, error)
}

// Bad — large monolithic interface defined alongside implementation
type StoreInterface interface {
    GetDriver(...)
    CreateDriver(...)
    GetBooking(...)
    CreateBooking(...)
    // ... dozens more
}
```

---

## Service Architecture

For microservice architectures:

- Each service owns its own schema and data. No shared databases.
- Inter-service communication uses well-defined contracts (gRPC, REST APIs).
- Client SDKs for inter-service calls live alongside the service they call.
- Services should be independently deployable and testable.
- Use an API gateway for external-facing orchestration.

### Adding a New Service

1. Create the service entry point following existing service patterns.
2. Apply standard middleware (auth, CORS, security headers, access logging).
3. Add database migrations if the service owns a schema.
4. Create a client SDK for inter-service use.
5. Register the service in the dev orchestrator and build system.

### Adding a New Module to an Existing Service

1. Create the module package with domain types and sentinel errors.
2. Add data access layer with all SQL constants and prepared statements.
3. Add an unexported interface for the module in the service orchestration layer.
4. Wire up the new store in the service constructor and entry point.
5. Verify the build compiles before committing.
