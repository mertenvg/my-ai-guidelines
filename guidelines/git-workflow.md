# Git Workflow

---

## Branching

- `main` is protected and should always be releasable.
- Use short-lived feature branches: `feat/<name>`, `fix/<name>`, `chore/<name>`.
- Rebase on latest `main` before requesting review.

---

## Commit Messages

Follow Conventional Commits:

```
feat: add driver document upload endpoint
fix: handle nil pointer in booking cancellation
docs: update README with new env variables
chore: bump dependencies
refactor: simplify service runner lifecycle
```

Guidelines:

- Use imperative mood: "add", "fix", "update" — not "added", "fixes".
- First line should be 72 characters or fewer.
- Include context in the body for non-trivial changes (what/why, not how).

---

## Pull Requests

- One logical change per PR. Split large changes into multiple PRs.
- Keep PRs small and focused — aim for under ~300 lines of diff.
- Provide a clear description: problem, approach, alternatives considered.
- Ensure build succeeds and tests pass locally before submitting.

### Issue-First Changes

- Open an issue describing the problem or proposal when scope is unclear.
- Reference the issue in the PR description and commit messages.

---

## Versioning

- Follow semantic versioning: `vMAJOR.MINOR.PATCH`.
- Avoid breaking changes in minor/patch releases.
- Document migration steps for any breaking changes.
