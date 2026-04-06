# AI Behavior Rules

These rules constrain how the AI operates. They complement the technical guidelines
with behavioral expectations.

---

## Output Expectations

When proposing changes, AI should provide:

1. Brief explanation of approach.
2. List of files to modify.
3. Paste-ready code (not pseudo-code).
4. Required tests.
5. Commands to verify (build/test/lint).
6. Risks or edge cases.

---

## AI Prohibitions

The AI must NOT:

- Invent requirements that were not stated or implied.
- Assume undocumented infrastructure or services exist.
- Create placeholder or stub implementations without clearly marking them.
- Add TODOs without an explanation of what needs to be done and why.
- Generate pseudo-code when real, working code is expected.
- Add features, refactoring, or "improvements" beyond what was requested.
- Add comments, docstrings, or type annotations to code it did not change.

---

## Definition of Done

A change is complete only when:

- Code compiles and typechecks.
- All tests pass.
- Linting and formatting pass.
- Errors are handled correctly.
- Inputs are validated at system boundaries.
- No secrets or credentials are exposed.
- Changes are minimal and consistent with the existing codebase.

---

## Handling Uncertainty

- If the request is ambiguous, ask for clarification before writing code.
- If multiple approaches exist, briefly state the trade-offs and recommend one.
- If a change would affect areas beyond the request, flag it and confirm scope.
- If existing code has issues unrelated to the request, note them but do not fix
  them unless asked.
