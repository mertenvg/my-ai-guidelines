# AI Engineering Guidelines

A comprehensive, reusable set of AI engineering guidelines compiled from real-world
production projects. These guidelines define how AI agents should operate when
generating or modifying code.

## Purpose

This repository is the single source of truth for AI coding guidelines across all
projects. Individual repositories should reference these guidelines rather than
maintaining their own copies.

## How to Use

### In a project with Claude Code

Add to your project's `CLAUDE.md`:

```markdown
Refer to the AI engineering guidelines at https://github.com/mertenvg/my-ai-guidelines/guidelines/
for the full set of rules. They apply to all work in this repository.
```

### In a project with Cursor

Reference the relevant guideline files in your `.cursorrules`.

### Cherry-picking

Each guideline file is self-contained. Reference only the files relevant to your
project's tech stack:

| File | When to include |
|---|---|
| `guidelines/principles.md` | Always |
| `guidelines/code-quality.md` | Always |
| `guidelines/security.md` | Always |
| `guidelines/architecture.md` | Always |
| `guidelines/testing.md` | Always |
| `guidelines/observability.md` | Always |
| `guidelines/performance.md` | Always |
| `guidelines/dependencies.md` | Always |
| `guidelines/api-compatibility.md` | Projects with APIs |
| `guidelines/git-workflow.md` | Always |
| `guidelines/ai-behavior.md` | Always |
| `guidelines/go.md` | Go projects |
| `guidelines/typescript-react.md` | TypeScript / React projects |
| `guidelines/sql-data.md` | Projects with SQL databases |
| `guidelines/protobuf-grpc.md` | Projects using protobuf / gRPC |

## Structure

```
guidelines/
  principles.md          Core objectives and philosophy
  code-quality.md        General code quality standards
  security.md            Security requirements (non-negotiable)
  architecture.md        Package structure and design patterns
  testing.md             Testing standards and patterns
  observability.md       Logging and error reporting
  performance.md         Performance and reliability
  dependencies.md        Dependency policy
  api-compatibility.md   API design and backward compatibility
  git-workflow.md        Branching, commits, and pull requests
  ai-behavior.md         AI-specific behavior rules and constraints
  go.md                  Go language guidelines
  typescript-react.md    TypeScript and React guidelines
  sql-data.md            SQL and data access patterns
  protobuf-grpc.md       Protocol Buffers and gRPC conventions
```

## Contributing

Open a PR to propose changes. Each guideline file has a clear scope — keep changes
focused on the relevant file. If a new topic area is needed, create a new file rather
than expanding an existing one.
