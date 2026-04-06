# TypeScript and React Guidelines

---

## Type Safety

- **Strict mode required.** Enable `noImplicitAny` and `strict` in `tsconfig.json`.
- **No `any` type.** Use `unknown` with type narrowing instead.
- Avoid unsafe non-null assertions (`!`). Use proper null checks.
- Keep public API types explicit and well-documented.
- Do not leak internal implementation types through public interfaces.

---

## Async Behavior

- Use `async/await` everywhere. Avoid raw `.then()` chains.
- Handle all promise rejections explicitly. Never swallow errors.
- Use `AbortController` / cancellation signals for long-running operations.

---

## React Components

- Use functional components with hooks exclusively. No class components.
- Pages live in `src/pages/`, shared UI in `src/components/`.
- API clients live in `src/lib/api/`.
- Avoid uncontrolled mutation of state or props.

---

## State Management

- Prefer dedicated state management (stores, context) over deep prop drilling.
- Use stores for state that must survive component unmount/remount.
- Use context-based stores when multiple sibling components need shared state.
- Use deep equality checks to prevent unnecessary re-renders.

---

## Forms

- Use declarative form components with context-based state.
- Validation rules are functions: `(value) => string` — return empty string if
  valid, error message if invalid.
- Separate form state management from UI components.

---

## Code Organization

- Group related code by feature/domain, not by technical role.
- Shared UI libraries should be npm workspace packages importable by sub-path
  (e.g., `@org/ui-lib/store`, `@org/ui-lib/form`).
- Keep utility libraries small and focused.

---

## Formatting

- Use Prettier for consistent formatting.
- Recommended defaults: `semi: true`, `singleQuote: true`, `trailingComma: "es5"`,
  `printWidth: 100`, `tabWidth: 2`.
- Use ESLint for code quality checks.
