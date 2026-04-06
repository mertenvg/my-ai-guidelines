# Dependency Policy

---

## Rules

- **Prefer standard library solutions.** Do not add a dependency for something the
  standard library handles well.
- **Do not add dependencies for trivial functionality.** A few lines of code are
  better than a new dependency.
- **Reuse existing project dependencies.** Before adding a new library, check if an
  existing dependency already provides the functionality.
- **Avoid introducing large frameworks.** Prefer small, focused libraries that do
  one thing well.
- **Pin dependency versions.** Use lock files and exact versions to ensure
  reproducible builds.

---

## When Adding a Dependency

Before introducing a new dependency, consider:

1. Does the standard library cover this?
2. Is there an existing dependency in the project that already does this?
3. Is the library well-maintained and actively supported?
4. What is the transitive dependency footprint?
5. Does it have a compatible license?
