# CLAUDE.md — my-ai-guidelines

## Project Purpose

This is the single source of truth for AI engineering guidelines across all of the
owner's projects. Individual repositories should reference these guidelines rather
than maintaining their own copies.

The guidelines were compiled from production codebases: a Go microservices platform
(rumi-black), a cryptographic messaging protocol (dmcn), a service orchestrator
(blade), and a web service (masarat.llc). They are not theoretical — they reflect
real patterns in active use.

## Structure

```
README.md                            How to use, cherry-picking table
guidelines/
  principles.md                      Core objectives, repo awareness, change scope
  code-quality.md                    Naming, error messages, defensive programming
  security.md                        Non-negotiable security rules
  architecture.md                    Module-based layout, DI, interface design
  testing.md                         Testing standards and assertion patterns
  observability.md                   Logging, error context, telemetry
  performance.md                     Concurrency, timeouts, query patterns
  dependencies.md                    Stdlib-first dependency policy
  api-compatibility.md               Backward compat, versioning
  git-workflow.md                    Branching, commits, PRs
  ai-behavior.md                     AI output expectations and constraints
  go.md                              Go-specific conventions
  typescript-react.md                TypeScript and React conventions
  sql-data.md                        SQL patterns (prepared statements, COALESCE, filters)
  protobuf-grpc.md                   buf v2, gRPC, deterministic serialization
```

## Owner Preferences

- **Module-based package structure is mandatory.** All code for a business domain
  (types, store, handler, tests) lives in one package. Never use classification-based
  layouts (models/, handlers/, repositories/). This is a strong, non-negotiable
  preference.
- Guidelines should be language-agnostic where possible, with language-specific
  detail in dedicated files.
- Each guideline file must be self-contained — projects cherry-pick the files
  relevant to their stack.
- No project-specific details (ports, env vars, service names) belong here. Those
  go in each project's own CLAUDE.md.

## Editing Guidelines

- Keep files focused on their stated scope. If a new topic area is needed, create a
  new file.
- Do not add redundant content across files. Cross-reference instead.
- Maintain the README.md cherry-picking table when adding or removing files.
- Use concrete code examples where they clarify a rule. Prefer Go and TypeScript for
  examples since those are the primary languages across projects.
- The tone is direct and imperative. These are rules, not suggestions.

## Tech Context

The owner's projects primarily use:

- **Backend:** Go (1.24–1.25), Gin, gRPC, PostgreSQL, protobuf (buf v2)
- **Frontend:** React 19, TypeScript 5.7, Material-UI v7, Vite
- **Testing:** stretchr/testify (Go), table-driven tests
- **Infra:** Docker, Make, blade (custom dev orchestrator)
- **Logging:** github.com/mertenvg/logr/v2

Guidelines may expand to cover additional languages or frameworks in the future.
