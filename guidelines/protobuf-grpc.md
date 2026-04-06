# Protocol Buffers and gRPC Conventions

---

## Proto File Organization

- Proto definitions live in a top-level `proto/` directory.
- Shared types (enums, common messages) go in `proto/common/`.
- Service-specific protos go in `proto/<service>/`.
- Generated code goes to a dedicated output directory (e.g.,
  `internal/proto/<pkg>/`).

---

## Code Generation

- Use `buf` (v2) for linting, breaking change detection, and code generation.
- Generated Go code should use `source_relative` paths.
- Run `make proto-gen` (or equivalent) to regenerate — never edit generated files
  manually.

### Example `buf.gen.yaml`

```yaml
version: v2
plugins:
  - remote: buf.build/protocolbuffers/go
    out: internal/proto
    opt: paths=source_relative
  - remote: buf.build/grpc/go
    out: internal/proto
    opt: paths=source_relative
```

---

## Lint and Breaking Change Detection

- Use `STANDARD` lint rules by default.
- Use `FILE` breaking change detection.
- Exclude generated code directories (`node_modules`, `vendor`) from linting.

---

## Serialization

- Use deterministic protobuf marshaling for any data that will be signed or hashed:
  `proto.MarshalOptions{Deterministic: true}`.
- Document this requirement in code comments when applicable.

---

## gRPC Service Design

- Define clear request/response messages — do not reuse domain models as API
  messages.
- Use pagination messages for list operations.
- Include proper error codes and status details.
- Client SDKs should wrap generated stubs with ergonomic, typed methods.
