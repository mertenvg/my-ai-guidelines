# Core Principles

These are the foundational rules that govern all AI-assisted code generation and
modification. They take precedence when other guidelines conflict.

---

## Primary Objectives

When generating or modifying code:

1. **Correctness over optimization.** Working code first; optimize only when measured.
2. **Readability over cleverness.** The next person reading your code might be you.
3. **Small, safe changes over large refactors.** Minimize blast radius.
4. **Preserve existing architecture** unless explicitly instructed otherwise.
5. **Follow existing patterns** before introducing new ones.

The AI must behave conservatively and production-minded.

---

## Repository Awareness (MANDATORY)

Before writing any code, the AI MUST:

- Inspect nearby files and similar implementations in the project.
- Reuse existing utilities, helpers, and abstractions.
- Follow established naming conventions.
- Match folder structure and dependency patterns.
- Use existing logging, error handling, and configuration systems.

Do NOT introduce new frameworks, patterns, or abstractions without clear necessity.

---

## Change Scope

AI changes must be:

- **Minimal** — only what is needed to satisfy the request.
- **Localized** — avoid touching unrelated code.
- **Backwards compatible** — unless instructed otherwise.

Avoid:

- Drive-by refactors of surrounding code.
- Style-only rewrites.
- Renaming unrelated symbols.
- Reformatting files not part of the change.
- Adding comments, docstrings, or type annotations to unchanged code.

If a refactor is necessary, explain why first.

---

## Simplicity

- Do not over-engineer. Only make changes that are directly requested or clearly
  necessary.
- Do not add features, error handling, or configurability beyond what was asked.
- Three similar lines of code are better than a premature abstraction.
- Do not design for hypothetical future requirements.
- Do not create helpers or utilities for one-time operations.
- Do not add backwards-compatibility shims when you can just change the code.
